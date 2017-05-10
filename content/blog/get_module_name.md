+++
date = "2017-05-10T15:00:43+08:00"
title = "python 中获取当前模块名"

+++

今天在看[sanic](https://github.com/channelcat/sanic)的实现时，看到 [app.py](https://github.com/channelcat/sanic/blob/master/sanic/app.py#L45)

```python
# Get name from previous stack frame
if name is None:
    frame_records = stack()[1]
    name = getmodulename(frame_records[1])
```

用`python`提供的`inspect`模块获取前一帧的模块名

`frame_records`是一个`FrameInfo`对象，打印出来如下:

```python
FrameInfo(frame=<frame object at 0x7f28a3732828>, filename='test.py', lineno=12, function='<module>', code_context=['print(foo(None))\n'], index=0)
```

由此可以获得当前的文件名，代码行数以及当前调用栈，现在能想到的是用在代码调试上。