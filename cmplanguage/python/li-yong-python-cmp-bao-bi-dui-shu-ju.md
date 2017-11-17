# 描述

```
cmp() 方法用于比较两个列表的元素。  语法： cmp(list1, list2)
```

# 返回值

```
如果比较的元素是同类型的,则比较其值,返回结果。
如果两个元素不是同一种类型,则检查它们是否是数字。
如果是数字,执行必要的数字强制类型转换,然后比较。
如果有一方的元素是数字,则另一方的元素"大"(数字是"最小的")
否则,通过类型名字的字母顺序进行比较。
如果有一个列表首先到达末尾,则另一个长一点的列表"大"。
如果我们用尽了两个列表的元素而且所 有元素都是相等的,那么结果就是个平局,就是说返回一个 0。
```

# 例

> 获取网路数据并与本地数据进行比对
>
> 实现方式： python + requests + cmp

```py
#coding=utf-8
__author__ = 'messageoom'

import re
import csv
import json
import requests

loginURL = "loginURL"
usernameUrl = "getdataURL"
crmCookies = {}
def loginCrm():
    """
    login crm & get cookies
    :return:
    """
    loginData = {"username":"username",
                 "password":password}
    reLogin = requests.post(url = loginURL,data = loginData)
    try:
        rejson = reLogin.json()
        #remrejson = str(rejson).replace("u", "")
        dupjson = json.dumps(rejson)
        json.loads(dupjson,encoding='utf-8')
    except:
        print "Module:%s()   %s"%(loginCrm.__name__,requestError()[0])
    else:
        originalCookie = str(reLogin.cookies)
        global crmCookies
        getCookieRegex = '([^ ]+)=([^ ]+)'
        cookies = re.findall(getCookieRegex,originalCookie)
        for i in range(len(cookies)):
            keys = cookies[i][0]
            values = cookies[i][1]
            cookieValue = {keys:values}
            crmCookies.update(cookieValue)
            i+=1

def getCrmUser():
    """
    get crm system user
    :return: getuser
    """
    crmData = {"pagesize":1200}
    usernameData = requests.post(url = usernameUrl,cookies = crmCookies,data = crmData)
    try:
        rejson = usernameData.json()
        dupjson = json.dumps(rejson)
        json.loads(dupjson,encoding='utf-8')
    except:
        print "Module:%s()   %s"%(getCrmUser.__name__,requestError()[0])
    else:
        rejson = usernameData.json()
        userClass = rejson[u'data'][u'data']
        getuser = []
        for i in range(len(userClass)):
            usernameDatas = userClass[i][u'username']
            getuser.append(usernameDatas)
        return getuser

def readECData():
    """
    get EC source data
    :return: column
    """
    with open('filepath\\filename.csv','rb') as csvfile:
        meReader = csv.reader(csvfile)
        column = [row[1] for row in meReader]
        columnhesder = column[0]
        column.remove(columnhesder)
        return column

def cmpData(crmData=None,sourceData=None):
    """
    Compare crmData with sourceData
    :param crmData:
    :param sourceData:
    :return:
    """
    if cmp(crmData,sourceData) == 0:
        print "%s"%requestError()[1]
    else:
        print "%s"%requestError()[2]


    # TODO complete other source data


def requestError():
    requestError = "【Error】:  please check request parameters"
    cmpError = "【Error】:  Incomplete import data"
    cmpYes = "【info】:  complete import data  YES!"
    return requestError,cmpYes,cmpError

if __name__ == "__main__":
    loginCrm()
    cmpData(getCrmUser(),readECData())
```



