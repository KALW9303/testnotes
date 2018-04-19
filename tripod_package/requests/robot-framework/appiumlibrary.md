### 以下是关于打开微信并登陆的小demo

> _注意 阅读以下事例前需对Robot Framework关键字有所了解 ：）_

### 步骤如下

* 启动Appium服务![](/assets/appiumRF.png)

* meAppiumFR.robot代码

```py
*** Settings ***
Library  AppiumLibrary

*** Test Cases ***

Open WeChat App
    [Documentation]    Opens and sign in WeChat app
    OPEN APPLICATION     http://127.0.0.1:4723/wd/hub    platformName=Android    platformVersion=7.1.1
    ...    deviceName=OPPO_R11    appPackage=com.tencent.mm    appActivity=com.tencent.mm.ui.LauncherUI

    click element    id=com.android.packageinstaller:id/permission_allow_button
    click element    id=com.android.packageinstaller:id/permission_allow_button
    click element    id=com.tencent.mm:id/d2z
    click element    com.tencent.mm:id/by6
    input value    xpath=//android.widget.EditText[contains(@text,"请填写微信号/QQ号/邮箱")]    messageoom
    input value    xpath=//android.widget.EditText[contains(@text,"请填写密码")]   qwaszx123
    click element    id=com.tencent.mm:id/bwn

    sleep  30
    close application
```

* 执行后运行效果如下，若要查看相应的报告及执行日志请查看**.html**文件![](/assets/exeresults.png)



