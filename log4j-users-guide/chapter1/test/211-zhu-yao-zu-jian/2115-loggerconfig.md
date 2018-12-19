# 2.1.1.5 LoggerConfig

LoggerConfig对象是在日志配置中声明Logger时创建的。LoggerConfig包含一组Filters，这些筛选器必须允许LogEvent在传递给任何Appender之前传递。它包含对应该用于处理事件的Appender集合的引用。

**日志级别**
LoggerConfigs将被分配一个日志级别。 内置级别包括TRACE，DEBUG，INFO，WARN，ERROR和FATAL。 Log4j 2还支持自定义日志级别。 获得更多粒度的另一种机制是使用Markers。

Log4j 1.x和Logback都具有“级别继承”的概念。 在Log4j 2中，Loggers和LoggerConfigs是两个不同的对象，因此这个概念的实现方式不同。 每个Logger引用相应的LoggerConfig，而LoggerConfig又可以引用其父级，从而实现相同的效果。

下面是五个表，其中包含各种已分配的级别值以及与每个Logger关联的结果级别。 请注意，在所有这些情况下，如果未配置根LoggerConfig，则会为其分配默认级别

示例1:

| logger名 | 分配的LoggerConfig | LoggerConfig 级别 |Logger 级别 |
| ------ | ------ | ------ |------ |
| root  | root | DEBUG  |DEBUG   |
| X     | root | DEBUG  |DEBUG   |
| X.Y   | root | DEBUG  |DEBUG   |
| X.Y.Z | root | DEBUG  |DEBUG   |
                                  
在上面的示例1中，仅配置了根记录器并具有日志级别。 所有其他Logger引用根LoggerConfig并使用其Level.

示例2:

| logger名 | 分配的LoggerConfig | LoggerConfig 级别 |Logger 级别 |
| ------ | ------ | ------ |------ |
| root  | root  | DEBUG  | DEBUG   |
| X     | X     | ERROR  | ERROR   |
| X.Y   | X.Y   | INFO   | INFO    |
| X.Y.Z | X.Y.Z | WARN   | WARN    |

在示例2中，所有记录器都具有已配置的LoggerConfig并从中获取其级别。
示例3:

| logger名 | 分配的LoggerConfig | LoggerConfig 级别 |Logger 级别 |
| ------ | ------ | ------ |------ |
| root  | root  | DEBUG  | DEBUG   |
| X     | X     | ERROR  | ERROR   |
| X.Y   | X     | ERROR  | ERROR   |
| X.Y.Z | X.Y.Z | WARN   | WARN    |

在示例3中，记录器root，X和X.Y.Z均具有已配置的具有相同名称的LoggerConfig。 Logger X.Y没有配置的具有匹配名称的LoggerConfig，因此使用LoggerConfig X的配置，因为这是LoggerConfig，其名称与Logger名称的开头最长匹配。

示例4:

| logger名 | 分配的LoggerConfig | LoggerConfig 级别 |Logger 级别 |
| ------ | ------ | ------ |------ |
| root  | root  | DEBUG  | DEBUG   |
| X     | X     | ERROR  | ERROR   |
| X.Y   | X     | ERROR  | ERROR   |
| X.Y.Z | X     | ERROR  | ERROR   |

在示例4中，记录器root和X每个都具有相同名称的Configured LoggerConfig。 记录器X.Y和X.Y.Z没有配置LoggerConfigs，因此从分配给它们的LoggerConfig获取它们的Level，因为它是LoggerConfig，其名称与Logger名称的开头最长匹配。

示例5:

| logger名 | 分配的LoggerConfig | LoggerConfig 级别 |Logger 级别 |
| ------ | ------ | ------ |------ |
| root  | root  | DEBUG  | DEBUG   |
| X     | X     | ERROR  | ERROR   |
| X.Y   | X.Y   | INFO   | INFO    |
| X.Y.Z | X     | ERROR  | ERROR   |

在示例5中，记录器root,X和X.Y都有一个具有相同名称的Configured  LoggerConfig。日志记录器X.Y.Z没有配置LoggerConfig，因此从分配给它的LoggerConfig X获取其级别，因为LoggerConfig的名称与日志记录器名称开头的匹配最长。它不与LoggerConfig X.Y关联，因为句点之后的标记必须精确匹配。

示例6:

| logger名 | 分配的LoggerConfig | LoggerConfig 级别 |Logger 级别 |
| ------ | ------ | ------ |------ |
| root  | root  | DEBUG  | DEBUG   |
| X     | X     | ERROR  | ERROR   |
| X.Y   | X.Y   |        | ERROR   |
| X.Y.Z | X.Y   |        | ERROR   |

在示例6中，LoggerConfig X.Y它没有配置级别，因此它从LoggerConfig X继承其级别.Logger X.Y.Z使用LoggerConfig X.Y，因为它没有名称完全匹配的LoggerConfig。 它也从LoggerConfig X继承了它的日志级别。

下表说明了级别过滤的工作原理。 在表中，垂直标题显示LogEvent的级别，而水平标题显示与相应的LoggerConfig关联的级别。 交集标识是否允许LogEvent被进行进一步处理（YES）或丢弃（NO）。

| EventLevel/LoggerConLevel | TRACE | DEBUG |INFO | WARN| ERROR|FATAL|OFF|
| ------ | ------ | ------ |------ |
| ALL   | YES| YES| YES| YES | YES| YES| NO | 
| TRACE | YES| NO | NO | NO  | NO | NO | NO | 
| DEBUG | YES| YES| NO | NO  | NO | NO | NO | 
| INFO  | YES| YES| YES| NO  | NO | NO | NO | 
| WARN  | YES| YES| YES| YES | NO | NO | NO | 
| ERROR | YES| YES| YES| YES | YES| NO | NO | 
| FATAL | YES| YES| YES| YES | YES| YES| NO | 
| OFF   | NO | NO | NO | NO  | NO | NO | NO | 











