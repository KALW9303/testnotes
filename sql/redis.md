# Resis简介

> Redis 是完全开源免费的，遵守BSD协议，是一个高性能的key-value数据库。支持的数据类型有字符串、列表、集合、哈希、有序集合。

### Redis官网 :  [https://redis.io/](https://redis.io/)

# Redis安装

* #### Ubuntu 系统安装 Redis

```
$sudo apt-get update
$sudo apt-get install redis-server
```

* 启动Redis

```
$ redis-server
```

* 查看 redis 是否启动？

```
$ redis-cli
```

* 以上命令将打开以下终端：

```
redis 127.0.0.1:6379>
```

* 127.0.0.1 是本机 IP ，6379 是 redis 服务端口。现在我们输入 PING 命令。

```
redis 127.0.0.1:6379> ping
PONG
```

以上说明我们已经在Ubuntu上成功安装了redis并已启动！

* #### Windows 系统安装 Redis

  > 官网给出的说明是并没有正式支持Windows平台，但是，Microsoft Open Tech组织开发并维护了面向Win64的Window的端口  ===》[Learn more](https://github.com/MSOpenTech/redis)

# Python操作Redis

* ### 使用pip/easy\_install安装redis模块

```bash
$ pip install redis
```

or

```
easy_install redis
```

* ### 操作Redis

### 



