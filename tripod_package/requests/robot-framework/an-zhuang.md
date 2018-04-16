# 部署Robot Framework/RIDE/selenium/requests环境

## 简介

```
RobotFramework是一种基于Python的可扩展关键字驱动自动化测试框架

RIDE是 RobotFramework框架原生的IDE集成环境（通俗理解：RobotFramework脚本编辑器）
```

## 部署安装

* 安装Robot Framework前的准备

```
python 2.x 、pip已安装
```

* 安装Robot Framework

```bash
> pip2 install robotframework
```

* 安装wxPython 

> RIDE是基于这个库开发的，且目前仅支持**wxPython 2.8.12.1Unicode**版本  下载后一键安装 ** **[**地址**](https://sourceforge.net/projects/wxpython/files/wxPython/2.8.12.1)

* 安装RIDE

```
pip install robotframework-ride
```

* 安装robotframework-selenium

```
> pip install robotframework-selenium2library
```

* 下载驱动并放置在`/usr/local/bin/`下

> [Chrome驱动下载地址](http://chromedriver.storage.googleapis.com/index.html)  （选择与Chrome浏览器版本对应的驱动）
>
> [Firefox驱动下载地址](https://github.com/mozilla/geckodriver/releases)

* 安装 robotframework-requests

```
> pip install -U robotframework-requests
```

## 启动RIDE

```
> py -2 D:\Python27\Scripts\ride.py
```

![](/assets/ride.png)

