# ActiveMQ

[官方下载地址](http://activemq.apache.org/download.html)

### 安装启动
- 第一步：把ActiveMQ 的压缩包上传到Linux系统
- 第二步：解压缩
- 第三步：启动
```
使用bin目录下的activemq命令启动：
[root@localhost bin]# ./activemq start
关闭：
[root@localhost bin]# ./activemq stop
查看状态：
[root@localhost bin]# ./activemq status

进入管理后台：http://IP:8161/admin
用户名：admin
密码：admin
```

登录用户名密码可在 `conf/jetty-realm.properties` 文件中修改

### ActiveMQ知识点

####  1. JMS(java message service： java消息服务)

> JMS是java的消息服务，JMS的客户端之间可以通过JMS服务进行异步的消息传输。

#### ActiveMQ消息类型:

* Point-to-Point(P2P) --点对点消息队列
* Publish/Subscribe(Pub/Sub) --发布订阅模型

####  p2p消息队列模型 

##### 1.涉及的概念

* 消息队列(Queue)
* 消息地址(Destination)
* 发送者(Sender):  只有一个发送者
* 接收者(Receiver): 只有一个接收者
* 会话(session)
* 链接(connection)
* 链接工厂(ConnectionFactory)
* JMStemplate

##### 2. 特点

* 每个消息只有一个消费者（Consumer）(即一旦被消费，消息就不再在消息队列中)

* 发送者和接收者之间在时间上没有依赖性，也就是说当发送者发送了消息之后，不管接收者有没有正在运行，它不会影响到消息被发送到队列

* 接收者在成功接收消息之后需向队列应答成功


####  Pub/Sub消息队列模型

##### 1. 涉及的概念

* 主题（Topic）
* 消息地址(Destination)
* 发布者(Publisher): 多个发布者
* 订阅者(Subscriber): 多个消费者
* 会话(session)
* 链接(connection)
* 链接工厂(ConnectionFactory)
* JmsTemplate

##### 2.Pub/Sub的特点

每个消息可以有多个消费者
发布者和订阅者之间有时间上的依赖性。针对某个主题（Topic）的订阅者，它必须创建一个订阅者之后，才能消费发布者的消息，而且为了消费消息，订阅者必须保持运行的状态。
为了缓和这样严格的时间相关性，**JMS允许订阅者创建一个可持久化的订阅。这样，即使订阅者没有被激活（运行**，它也能接收到发布者的消息。



#### 编程模型

*  ConnectionFactory

> 创建Connection对象的工厂，针对两种不同的jms消息模型，分别有QueueConnectionFactory和TopicConnectionFactory两种。可以通过JNDI来查找ConnectionFactory对象。

*  Destination

> Destination的意思是消息生产者的消息发送目标或者说消息消费者的消息来源。对于消息生产者来说，它的Destination是某个队列（Queue）或某个主题（Topic）;对于消息消费者来说，它的Destination也是某个队列或主题（即消息来源）。

所以，Destination实际上就是两种类型的对象：Queue、Topic可以通过JNDI来查找Destination。

* Connection

> Connection表示在客户端和JMS系统之间建立的链接（对TCP/IP socket的包装）。Connection可以产生一个或多个Session。跟ConnectionFactory一样，Connection也有两种类型：QueueConnection和TopicConnection。

* Session

> Session是我们操作消息的接口。可以通过session创建生产者、消费者、消息等。Session提供了事务的功能。当我们需要使用session发送/接收多个消息时，可以将这些发送/接收动作放到一个事务中。同样，也分QueueSession和TopicSession。

* 消息的生产者

> 消息生产者由Session创建，并用于将消息发送到Destination。同样，消息生产者分两种类型：QueueSender和TopicPublisher。可以调用消息生产者的方法（send或publish方法）发送消息。

* 消息消费者

> 消息消费者由Session创建，用于接收被发送到Destination的消息。两种类型：QueueReceiver和TopicSubscriber。可分别通过session的createReceiver(Queue)或createSubscriber(Topic)来创建。当然，也可以session的creatDurableSubscriber方法来创建持久化的订阅者。

* MessageListener

消息监听器。如果注册了消息监听器，一旦消息到达，将自动调用监听器的onMessage方法。EJB中的MDB（Message-Driven Bean）就是一种MessageListener。




