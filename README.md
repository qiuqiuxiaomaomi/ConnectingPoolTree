# ConnectingPoolTree
数据库连接池技术

![](https://i.imgur.com/y6f6El4.png)

<pre>
LRU：
</pre>

<pre>
PSCache(PreparedStatementCache)
      打开PSCache，则PreparedStatement会被缓存起来重复执行。
</pre>

<pre>
PSCache-Oracle-Optimized
</pre>

<pre>
ExceptionSorter
      如果一个连接产生了不可恢复的错误，必须立刻从连接池中去掉，否则会连续的产生大量错误。
</pre>

<pre>
      Oracle支持游标，一个PreparedStatement对应服务器一个游标，如果PreparedStatement
   被缓存起来重复执行，PreparedStatement没有被关闭，服务器端的游标就不会被关闭，在类似
   Select * from table where id = ?这样的场景下，性能时一个数量级的提升。
</pre>

<pre>
Druid的特性分析
      1）可以监控数据库性能，Druid内置提供了功能强大的StatFilter插件，能够详细统计SQL的
         执行性能，这对于线上分析数据库访问性能有帮助。
      2）数据库密码加密
             直接把数据库密码写在配置文件中，这是不好的，Druid支持password加密
      3）SQL执行日志
             Druid提供不同的LogFilter，监控应用的数据库访问情况。
      5）扩展JDBC，如果有对JDBC层编程的需求，可以通过Druid提供的Filter机制，很方便编写
         JDBC层的扩展插件。
</pre>

<pre>
连接池最大连接数，最小连接数设置问题
      1）为什么不大一点
         1）连接数需要内存支持
         2）CPU负荷
         3）线程上下文切换
         5）CPU核数固定
      2）为什么不小一点
         1）造成连接排队，系统变慢
         2）连接经常打开，关闭，性能差
</pre>