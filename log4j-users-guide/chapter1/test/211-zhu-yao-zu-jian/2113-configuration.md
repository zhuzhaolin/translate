# 2.1.1.3 Configuration

每个LoggEnrices都有一个活动的配置。配置包含所有Appenders、上下文范围的Filters、LoggerConfigs，并包含对StrSubstitutor的引用。在重新配置期间，将存在两个配置对象。一旦所有日志记录器都被重定向到新的配置，旧的配置将被停止并丢弃。