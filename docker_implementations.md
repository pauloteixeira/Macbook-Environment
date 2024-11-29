# DOCKER IMPLEMENTATION'S TIPS
In this document will be possible to set some docker implementation tips to use day by day.

## RabbitMQ with management
```VIM
docker run -d -p 15672:15672 -p 5672:5672 --name rabiitmq rabbitmq:3-management
```
The 15672 port is to the management portal and the 5672 port is to the queues.
To access the portal the url is: http://localhost:15672/
The login and pass is guest

------------------------------------------------------------------------------------------------
