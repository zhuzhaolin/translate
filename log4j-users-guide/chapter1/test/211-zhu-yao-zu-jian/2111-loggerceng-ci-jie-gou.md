# Logger 层次结构

与普通System.out.println相比，任何日志记录API的首要优势在于它能够禁用某些日志语句，同时允许其他人不受阻碍地打印。 这种能力假定对日志记录空间（即所有可能的日志记录语句的空间）进行了分类根据一些开发人员选择的标准。

在Log4j 1.x中，Logger层次结构通过Loggers之间的关系进行维护。 在Log4j 2中，这种关系不再存在。 而是在LoggerConfig对象之间的关系中维护层次结构。

**Named Hierarchy**
*如果LoggerConfig的名称后跟一个点是后代logger名称的前缀，则称其为另一个LoggerConfig的祖先。 如果LoggerConfig本身与后代LoggerConfig之间没有祖先，则称LoggerConfig是子LoggerConfig的父节点。*

例如，名为“com.foo”的LoggerConfig是名为“com.foo.Bar”的LoggerConfig的父级。类似地，“java”是“java.util”的父级和“java.util.Vector”的祖先。 大多数开发人员都应该熟悉这种命名方案。
根LoggerConfig位于LoggerConfig层次结构的顶部。 它的特殊之处在于它始终存在，并且它是每个层次结构的一部分。 可以如下获得直接链接到根LoggerConfig的logger:
 ` Logger logger = LogManager.getLogger(LogManager.ROOT_LOGGER_NAME);`

或者，下面方法更简单:
`Logger logger = LogManager.getRootLogger();`


通过传递所需Logger的名称，可以使用LogManager.getLogger静态方法检索所有其他Logger。 有关Logging API的更多信息可以在Log4j 2 API中找到.