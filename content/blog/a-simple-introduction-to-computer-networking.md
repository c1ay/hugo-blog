+++
date = "2017-02-17T20:41:19+08:00"
title = "（转）a simple introduction to computer networking"

+++

大多数关于计算机网络的都是一大堆首字母缩写。忘掉这些配置细节----你有什么看法？

* 网络是关于通信
* 文本是最简单的沟通方式
* 协议是读和写这些文本的标准

在细节下面，网络是一个IM对话。这是我希望有人告诉我，当学习如何计算机通信。

### *TCP: 文本层*

传输控制协议（TCP）让我们有了很方便在两台计算机之间发送文本的错觉。 TCP依赖于较低级别并且可以发送二进制数据，但是现在忽略它：

* **TCP允许我们在计算机之间进行即时消息**

We IM with Telnet, the ‘notepad’ of networking: telnet sends and receives plain text using TCP. It’s a chat client peacefully free of ads and unsolicited buddy requests.