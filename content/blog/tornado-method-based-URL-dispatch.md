+++
date = "2016-08-17T14:33:27+08:00"
title = "tornado method-based URL dispatch"

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

<script src="https://gist.github.com/c1ay/06554e6fc6e36803b40d2359ff1adbf1.js"></script>

> 参考: http://code.activestate.com/recipes/576958/
