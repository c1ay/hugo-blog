+++
date = "2016-08-17T14:33:27+08:00"
title = "tornado method based URL dispatch"

+++


### 基于 method 的URL 分发

#### 问题:

如果我要完成同一层级下不同url的get请求, 只能写成这样:

```python
from tornado.web import RequestHandler

class InterfaceOne(RequestHandler):

    def get(self):
        self.write('InterfaceOne')

class InterfaceTwo(RequestHandler):

    def get(self):
        self.write('InterfaceTwo')

application = tornado.web.Application([
    (r"/level_1/interface_one", InterfaceOne),
    (r"/level_1/interface_two", InterfaceTwo),
])

```

我不想每个接口都要写一个类去处理，而这些请求只需要处理`GET`请求，还要为每个类去注册`url`

有没有什么解决方案去处理呢，加上我又很懒，最好`url`也能自己生成. 像这样:

```python
class Level:

    def interface_one(self):
        # 处理 url /level/interface_one 的请求
        pass

    def interface_two(self):
        # 处理 url /level/interface_two 的请求
        pass
```

#### 解决方案:

最终效果
```python

class Test(MethodDispatcher):

    def interface_one(self):
        # 处理 url /test/interface_one 的请求
        self.write(self.request.path)

    def interface_two(self):
        # 处理 url /test/interface_two 的请求
        self.write(self.request.path)

application = tornado.web.Application([
    (r"/test/.*", Test),
])

```

`MethodDispatcher` 最终的实现

```python
class MethodDispatcher(RequestHandler):

    allow_methods = ()

    def set_default_headers(self):
        # 这里是允许跨域请求
        origin = None
        if self.request.headers.get('Origin'):
            origin = self.request.headers['Origin']
        else:
            url = self.request.headers.get('Referer')
            if url:
                import re
                pat = re.compile(r'(http|https)://.+/')
                match = pat.search(url)
                origin = match.group()[0:-1]
        if origin:
            self.set_header('Access-Control-Allow-Origin', origin)
        self.set_header('Access-Control-Allow-Methods', 'POST, GET, OPTIONS')
        self.set_header('Access-Control-Max-Age', 1000)
        self.set_header('Access-Control-Allow-Headers', '*')
        self.set_header('Access-Control-Allow-Credentials', 'true')

    def _delist_arguments(self, args):
        # 将GET 参数转化成 参数
        for arg, value in args.items():
            if len(value) == 1:
                args[arg] = value[0]
        return args

    def _dispatcher(self):
        args = None

        if self.request.arguments:
            args = self._delist_arguments(self.request.arguments)

        path = self.request.uri.split('?')[0]
        method = path.split('/')[-1]
        if not method.startswith('_'):
            if method not in self.allow_methods:
                raise HTTPError(404)
            func = getattr(self, method, None)
            if func:
                if args:
                    return func(**args)
                else:
                    return func()
            else:
                raise HTTPError(404)
        else:
            raise HTTPError(404)

    def get(self):
        self.method = 'GET'
        return self._dispatcher()

    def post(self):
        self.method = 'POST'
        return self._dispatcher()

    def options(self):
        self.set_status(204)
        self.finish()

```

> 参考: http://code.activestate.com/recipes/576958/