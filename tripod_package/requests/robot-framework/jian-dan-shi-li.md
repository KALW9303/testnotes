### demos

> 阅读以下事例前需对Robot Framework关键字有所了解

* **事例1：调用python程序**

```py
$ cat count.py    
def add(a,b):
    return a + b
---------------------------------------------------------
$ cat cbpyscripts.robot 
*** Test Cases ***

test case
    Import Library      /root/messageoom/robotFR/count.py
    ${a}    Evaluate    int(5)
    ${b}    Evaluate    int(10)
    ${add}    add    ${a}    ${b}
    log    ${add}
```

运行结果![](/assets/QQ截图20180416173030.png)![](/assets/QQ截图20180416173131.png)

* **事例2：用Chrome浏览器打开百度搜索 **

```py
$ cat test_searchRF.robot
*** Settings ***
Library           SeleniumLibrary

*** Test Cases ***
Baidu search case
    Open Browser    http://www.baidu.com    chrome
    Input text      id=kw    robot framework
    click button    id=su   
    close Browser
```

运行结果![](/assets/运行结果r.png)![](/assets/QQ截图20180416173634.png)_**注意** 这个事例遇到两个坑： 一个是kali安装的Chrome浏览器不能用root用户打开，另一个是切换普通用户运行脚本不能调起桌面（处理方式：切换普通用户前执行 `#xhost +`）_

