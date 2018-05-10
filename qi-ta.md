* Python3环境下Unicode转中文

在python服务端返回的数据进行处理数据时，难免遇到Unicode。以下是关于python3环境下Unicode转中文做法

```py
if isinstance(Object, bytes):
    Object.decode('unicode_escape')
elif isinstance(Object, str):
    Object.encode('latin-1').decode('unicode_escape')
elif ......
```



