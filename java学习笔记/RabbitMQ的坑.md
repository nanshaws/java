# RabbitMQ的坑

## 一、helloworld的例子中出现的坑

使用云服务器的小伙伴们，在发送Helloworld的例子中

RabbitMQ的管理界面端口是15672，但是rabbitmq的端口是5672，如果不开放安全组，是发送不过去的哦

