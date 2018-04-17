# Jmeter监控服务器性能

### 性能测试常关注的指标

* ###### 服务本身： 并发、响应时间、QPS
* ###### 服务器的资源情况：CPU、Memory、Disk I/O、network I/O等

### 插件下载

* 下载**JMeterPlugins-Standard**和**JMeterPlugins-Extras**解压并将jar包放置Jmeter客户端lib/ext下
* 下载两个jar包（[**jmeter-plugins-perfmon**](http://www.mvnjar.com/kg.apc/jmeter-plugins-perfmon/jar.html)** 、**[**jmeter-plugins-cmn-jmeter**](http://www.mvnjar.com/kg.apc/jmeter-plugins-cmn-jmeter/jar.html)）并放置jmeter客户端lib/ext下
* 下载服务端代理 [**ServerAgent**](https://github.com/undera/perfmon-agent/releases/download/2.2.3/ServerAgent-2.2.3.zip) 解压后进入目录
  * Windows 双击**startAgent.bat**
  * Linux **./startAgent.sh** 或者**source startAgent.sh **默认端口4444![](/assets/startAgent.png)

### Jmeter客户端监听

* 打开Jmeter客户端添加线程组（线程组循环次数勾选**永远**），该线程组下添加若干条http请求
* 添加监听器Permon Metrics Collector，servers to moniter模块表格中HOST/IP更改被测主机的IP![](/assets/servermoniternew.png)![](/assets/serverAgentLog.png)

## _综合性能测试后续添加 ：TODO_



