#### 开始测试前的准备工作

* 主机已安装Appium
* 真机已打开开发者模式并通过USB连接至主机

#### 启动appium服务

* CMD 输入`adb devices -l`获取真机UUID

* 启动appium服务![](/assets/startAppium.png)

#### 代码执行

以下事例是登录微信的小demo

* 获取App Package及Activity![](/assets/getAppact.png)
* 事例代码

```py
# -*- coding:utf-8 -*-

__author__ = 'messageoom'
import os
import time
from appium import webdriver

PATH = lambda p: os.path.abspath(os.path.join(os.path.dirname(__file__), p))

desired_caps = {}
desired_caps['platformName'] = 'Android'
desired_caps['platformVersion'] = '7.1.1'
desired_caps['deviceName'] = 'OPPO_R11'
desired_caps['app'] = PATH(r'E:\55219a29b87906c894acd8dadfeaa899.apk')
desired_caps['appPackage'] = 'com.tencent.mm'
desired_caps['appActivity'] = 'com.tencent.mm.ui.LauncherUI'

driver = webdriver.Remote('http://localhost:4723/wd/hub', desired_caps)

driver.find_element_by_android_uiautomator('new UiSelector().className("android.widget.Button").text("始终允许")').click()
driver.find_element_by_android_uiautomator('new UiSelector().className("android.widget.Button").text("始终允许")').click()
driver.find_element_by_android_uiautomator('new UiSelector().className("android.widget.Button").text("登录")').click()
driver.find_element_by_android_uiautomator('new UiSelector().className("android.widget.Button").text("用微信号/QQ号/邮箱登录")').click()
time.sleep(1)
driver.find_element_by_android_uiautomator('new UiSelector().textContains("请填写微信号/QQ号/邮箱")').set_value("meTEST")
driver.find_element_by_android_uiautomator('new UiSelector().className("android.widget.EditText").text("请填写密码")').set_value("abc123")
time.sleep(1)
driver.quit()
```

_**注意 ： appium 1.6.x 用send\_keys输入字符会报错，改用set\_value即可**_

