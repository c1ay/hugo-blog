+++
date = "2017-05-23T17:16:04+08:00"
title = "Learn GraphQL -了解GraphQl（一）"

+++

#### GraphQL 简介:

GraphQL是Facebook出品的应用层查询语言。你可以用GraphQL明确的定义基于基于图形的schema。客户端就可以请求它所需要的数据集了。

![](https://cldup.com/ysnmIMhqRU.png)

所以，你不需要因为客户端请求数据的变动更改你的后端，这简单的解决了使用REST API的最大的问题之一。

GraphQL也允许让客户端高效的批量获取数据，比如下面就是一个GraphQL查询：

```json
{
  latestPost {
    _id,
    title,
    content,
    author {
      name
    },
    comments {
      content,
      author {
        name
      }
    }
  }
}
```

这就是一个获取博客文章、评论以及作者信息的GraphQL请求，这是上面请求的结果:

```json
{
  "data": {
    "latestPost": {
      "_id": "03390abb5570ce03ae524397d215713b",
      "title": "New Feature: Tracking Error Status with Kadira",
      "content": "Here is a common feedback we received from our users ...",
      "author": {
        "name": "Pahan Sarathchandra"
      },
      "comments": [
        {
          "content": "This is a very good blog post",
          "author": {
            "name": "Arunoda Susiripala"
          }
        },
        {
          "content": "Keep up the good work",
          "author": {
            "name": "Kasun Indi"
          }
        }
      ]
    }
  }
}
```

如果使用REST, 则需要调用多个API 请求来获取这些数据。

**GraphQL 是一个规范（标准）**

所以，它可以用于任何平台，任何编程语言。它有一个由Facebook维护的[JavaScript](https://github.com/graphql/graphql-js)实现参考。也有很多由社区维护的其它语言[实现](https://github.com/chentsulin/awesome-graphql#table-of-contents)

> 这里是标准: [http://facebook.github.io/graphql/](http://facebook.github.io/graphql/)

一旦你使用了GraphQL，你会想在所有项目都使用它