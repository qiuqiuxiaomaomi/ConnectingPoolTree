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