### demos

> 阅读以下事例前需对Robot Framework关键字有所了解

* 事例1：调用python程序

```
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

* 事例2：用Chrome浏览器打开百度搜索 

```
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

运行结果![](/assets/运行结果r.png)![](/assets/QQ截图20180416173634.png)

