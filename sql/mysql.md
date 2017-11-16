# 安装

* ### ubuntu

  ```
  检测是否安装(没有显示已安装结果，则没有安装。)
  $ sudo netstat -tap | grep mysql
  安装
  $ sudo apt-get install mysql-server mysql-client
  ```

## 授权远程登录

* 第一步 在配置文件中找到 mysqld.cnf 将以下语句注释掉

```
$ sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf
bind-address = 127.0.0.1
```

* 第二步  root用户登录数据库，授权

```
$ mysql --password=password --user=username
$ grant all on *.* to username@'%' identified by password;
$ flush privileges;
```

```
"*.*"：第一个*代表数据库名；第二个*代表表名。这里的意思是所有数据库里的所有表都授权给用户。  
username：需要授予的账号。    
“%”：表示授权的用户IP可以指定，这里代表任意的IP地址都能访问MySQL数据库。    
“password”：分配账号对应的密码，这里密码自己替换成你的t帐号密码。
```

* 第三步 重启数据库服务

```bash
$ systemctl restart mysql.service
```



