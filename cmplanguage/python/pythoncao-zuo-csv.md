# Python操作CSV文件

> 平常我们可能会对CSV，execel文件进行读写操作，故将自己用到的些做了些许笔记

* ### CSV写入操作

```py
import csv
import codecs
csvfile = file('csv_test.csv', 'wb')
#处理中文乱码
csvfile.write(codecs.BOM_UTF8)
writer = csv.writer(csvfile)
writer.writerow(["姓名", "电话", "QQ", "微信","身份证号",""])
    for i in range(0,200):
    data = [('MS%s'%i, '', '891110%s'%i, 'MSweixin%s'%i, '', '')]
    writer.writerows(data)
csvfile.close()
```



