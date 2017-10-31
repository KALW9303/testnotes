# Git

> Git是一个[免费的开源](https://git-scm.com/about/free-and-open-source)分布式版本控制系统，旨在以高效和高效的方式处理从小到大的项目。
>
> 官方解释
>
> ```
>     Git is a free and open source distributed version control system designed to handle everything from small to 
> very large projects with speed and efficiency.
> ```
>
> [官网: https://git-scm.com](https://git-scm.com)





### Git修改远程仓库地址

#### 方法有三种

* 直接修改命令

```bash
$ git remote set-url origin [url]
```

* 先删除 再添加

```bash
$ git remote rm origin
$ git remote add origin [url]
```

* 直接修改config文件



