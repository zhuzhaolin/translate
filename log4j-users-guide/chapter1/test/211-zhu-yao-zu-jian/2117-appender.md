# 2.1.1.7 Appender

根据日志记录程序有选择地启用或禁用日志记录请求的能力只是其中的一部分。Log4j允许将日志请求打印到多个目的地。在log4j中，输出目的地称为Appender。目前，存在用于控制台、文件、远程套接字服务器、Apache Flume、JMS、远程UNIX Syslog守护进程和各种数据库api的appenders。有关可用的各种类型appender的更多详细信息，请参见appender一节。Logger可以绑定多个Appender。