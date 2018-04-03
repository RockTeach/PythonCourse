# Logging

[https://docs.djangoproject.com/zh-hans/2.0/topics/logging/](https://docs.djangoproject.com/zh-hans/2.0/topics/logging/)

Django使用了Python中内建的logging模型实现了Django系统的日志系统。



### 核心成员

* Loggers
  * 日志系统的入口
  * 日志有级别，级别标识日志信息将被怎么处理
    * DEBUG
    * INFO
    * WARNING
    * ERROR
    * CRITICAL
* Handlers
  * logger消息的处理者
  * 决定每条消息如何处理
* Filters
  * 对于从logger传递handler的日志记录进行额外的过滤控制
* Formatters
  * 对日志的格式进行格式化



