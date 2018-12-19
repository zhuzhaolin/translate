# 2.1.1.4 Logger
如前所述，Loggers是通过调用LogManager.getLogger创建的。 Logger本身不执行任何直接操作。 它只是一个名称，并与LoggerConfig相关联。 它扩展了AbstractLogger并实现了所需的方法。 随着配置的修改，Logger可能会与不同的LoggerConfig关联，从而导致其行为被修改

**检索 Loggers**
使用相同的名称调用LogManager.getLogger方法将始终返回对完全相同的Logger对象的引用

例如：
```
Logger x = LogManager.getLogger("wombat");
Logger y = LogManager.getLogger("wombat");
```

x和y引用的是完全相同的Logger对象。
log4j环境的配置通常在应用程序初始化时完成。 首选方法是读取配置文件。 这在配置章节中讨论。

Log4j可以轻松地按软件组件命名Loggers。 这可以通过在每个类中实例化Logger来实现，其中Logger名称等于类的完全限定名称。 这是定义Logger的有用且直接的方法。 由于日志输出带有生成Logger的名称，因此该命名策略可以轻松识别日志消息的来源。 但是，这只是命名记录器的一种可能的策略，尽管很常见。 Log4j不限制可能的记录器集。 开发人员可以根据需要自由命名记录器。

由于以Logger所属类的名称命名Logger是一种非常常见的习惯用法，因此提供了方便的方法LogManager.getLogger()来自动使用调用类的完全限定类名作为Logger名称。

尽管如此，根据Logger所在的类来命名日志记录器似乎是目前已知的最佳策略