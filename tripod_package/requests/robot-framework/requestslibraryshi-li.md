### 以下是关于请求baidu并验证是否请求成功的小DEMO

> _注意 阅读以下事例前需对Robot Framework关键字有所了解 ：）_

* meRequestsRF.robot代码如下

```py
*** Settings ***
Library  AppiumLibrary
    Library  RequestsLibrary

*** Test Cases ***

Requests URL RESTF
    [Documentation]    Request Baidu and get response code
    create session  baidu  https://www.baidu.com  #verify=False
    ${rep}=  GET REQUEST  baidu  /
    ${code_ZH}  set variable  请求响应码:
    ${console_info}  catenate  ${code_ZH}  ${rep.status_code}
    log to console  ${console_info}
    Should Be Equal As Strings    ${rep.status_code}    200
```

* 执行后运行效果如下，若要查看相应的报告及执行日志请查看**.html文件**![](/assets/requestsRF_log.png)



