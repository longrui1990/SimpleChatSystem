# SimpleChatSystem
基于TCP的简单聊天系统
包含客户端程和服务端独立的线程，即一个主线程和一个子线程
【1】客户端主线程  ChatClient.java
    该程序根据启动时输入用户名参数，负责启动客户端子线程，由子线程建立客户端和服务端连接。在主线程中需要循环读取键盘输入，将输入的信息循环发送给服务端，交由服务端来转发给客户端
【2】客户端子线程  ClientThread.java
    该线程封装了客户端和服务端的所有操作
    a.在构造函数中，根据用户名创建于服务端连接，然后发送用户名给服务端进行注册。
    b.在线程主函数中，循环读取服务端发送的消息，并显示到控制台。
    c.还应有一个发送消息函数，外部的主线程在接收到键盘输入后，调用该函数给服务端发送消息。
    d.关闭函数：在客户端键盘输入bye命令后，关闭客户端和服务端的连接。
【3】服务端主线程  ChatServer.java
    该类负责启动服务端，并负责监听客户端的请求，在收到新的用户端后，交给子线程处理。
【4】服务端子线程  ServerThread.java
    该线程负责处理客户端的输入/输出的消息转发任务，因此需要包含以下功能。
    a.在构造函数中，建立与客户端的输入/输出流，并在第一次建立连接时读取客户端发送的用户名，并将用户添加到客户端列表中。
    b.在线程主函数中，读取客户端的输入数据，如果发送的消息是bye，则退出监听关闭该客户端，否则，根据命令格式进行解析。冒号
    (:)前面的部分为用户名，根据该用户名在客户端列表中找到对应的客户端处理线程，发送数据给客户端。
    c.发送数据函数:在收到用户消息进行转发时调用。
