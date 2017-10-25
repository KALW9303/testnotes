# requests获取请求的cookies
> 我们访问的网页（登录）的时候，cookies大都是经过加密处理后的数据。返回的字符串完全看不懂！不过对于它我们不需要看懂也能将它转换后作为requests请求的认证参数，具体思想是将requests请求获取的原始cookies解析为字典格式数据的Cookies，然后将获取的Cookies放在requests请求参数中即可。

## 获取cookies的代码如下

```
reLogin = requests.post(url = loginURL,data = loginData)
#定义字典接收获取的cookies
crmCookies = {}
# cookie中的值基本以键值对形式存在，所以我们先定义一个正则表达式
getCookieRegex = '([^ ]+)=([^ ]+)'
# re包找出requests<cookies>中返回符合我们定义正则的值
cookies = re.findall(getCookieRegex,originalCookie)
# 遍历出cookies中key及对应value存放在crmCookies
for i in range(len(cookies)):
    keys = cookies[i][0]
    values = cookies[i][1]
    cookieValue = {keys:values}
    crmCookies.update(cookieValue)
    i+=1
```
