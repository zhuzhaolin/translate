+\# 2.1.1 主要组件  
Log4J使用类结构如下图所示  
![](/assets/1542516098%281%29.png)

使用Log4j 2 API的应用程序将从LogManager请求具有特定名称的Logger。LogManager将找到相应的LoggerContext，然后从中获取Logger。 如果必须创建Logger，它将与LoggerConfig关联，LoggerConfig包含与Logger相同的名称，这名称来自父包的名称或根LoggerConfig。 LoggerConfig对象是从配置中的Logger声明创建的。 LoggerConfig与实际传递LogEvents的Appender相关联。

