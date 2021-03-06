# zeppelin-server

```md
项目入口，通过Jetty内嵌服务器提供WebSocekt服务和RESTful服务，并且提供了基本的权限验证服务。
ZeppelinServer是各个组件的”组装者”，它是系统的主入口。

Apache Zeppelin的服务器模块由三部分组成：
处理 rest / websocket，存储和加载数据以及管理解释器。
```
* 职责
```md
1. 内嵌 jetty 服务器，支持以 WebSocket 和 REST 两种方式对外暴露系统功能 
2. 创建 NotebookServer 实例，建立起处理 WebSocket Connection 和 消息处理的服务端 
3. 创建 Notebook 需要的相关依赖，如 Note 持久化服务(NotebookRepo)、
    Note 的全文索引服务（SearchService），并完成向 Note、Paragraph 的注入。 
4. Note 权限配置文件的加载以及初始化 
5. InterpreterFactory 的初始化 
6. 初始化动态依赖加载器(DependencyResolver)
```

## Class

* [ZeppelinServer](ZeppelinServer.md)
![](../../pic/ZeppelinServer-UML.jpg)
* [NotebookServer](NotebookServer.md)
![](../../pic/NotebookServer.jpg)

* NotebookSocket 

![](../../pic/NotebookSocket-UML.png)

* NotebookWebSocketCreator (Responsible to create the WebSockets for the NotebookServer.)
* NotebookSocketListener
* ConnectionManager (managing websocket connections)
