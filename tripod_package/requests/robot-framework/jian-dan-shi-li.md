### demo

* 事例1：用Chrome浏览器打开百度搜索 

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

运行结果![](/assets/运行结果r.png)

