# Scrapy

> Scrapy是一个为了爬取网站数据，提取结构性数据而编写的应用框架。 可以应用在包括数据挖掘，信息处理或存储历史数据等一系列的程序中。

#### [Scrapy官网](https://scrapy.org)

使用pip安装

```py
pip install Scrapy
```

### scrapy 事例

* 创建一个scrapy项目
* 爬取某网站楼盘相关信息并存储在本地数据库

###### 注意 开始之前你需要注意以下几点

1. 已配置好python环境
2. 已安装Scrapy
3. 已安装beautifulsoup
4. 已安装sqlite服务

### 创建项目

> 在开始爬取之前，您必须创建一个新的Scrapy项目。 进入您打算存储代码的目录中，运行下列命令

```
scrapy startproject loupaninfo
```

该命令将创建包含以下内容的loupan\_info目录

```
F:.
│  scrapy.cfg
│
└─loupaninfo
    │  items.py
    │  middlewares.py
    │  pipelines.py
    │  settings.py
    │  __init__.py
    │
    ├─spiders
       │  __init__.py
       ......
```

### 编写代码

> 爬取数据及将获取的数据写进本地数据库

* 下为爬取数据文件，保存在loupaninfo/spiders目录下的getLoupanData.py文件中:

```py
# -*- coding: utf-8 -*-
__author__ = 'messageoom'

import re
import time
import scrapy
from bs4 import BeautifulSoup
import requests

from loupaninfo.public.meSqlite import meDB



class loupandata(scrapy.Spider):
    name = "loupaninfo"
    allowed_domains = "https://www.xxx.com/"
    start_urls = []
    for i in range(1,60):
        start_urls.append("https://www.xxx.com/loupan/all/p%d/"%i)

    def parse(self, response):
        """
        抓取数据解析后写入数据库
        """
        soup = BeautifulSoup(response.text, 'lxml')
        lp_list = soup.find_all(class_ = "key-list")
        via_content = soup.find_all(class_ = "favor-pos"  )

        for item in via_content:
            code = item["href"].split("/")[-1][:6]
            real_href = "https://cd.fang.anjuke.com/loupan/canshu-{}.html?from=loupan_index_more".format(code)
            res = requests.get(real_href)
            soup_lp = BeautifulSoup(res.text,"lxml")
            lp_parameter = re.findall(r'<div class="name">(.*?)</div>', str(soup_lp)) # Property parameter information
            lp_desc = soup_lp.find_all(class_ = "des")

            lp_details = {}
            meDB().crtTABLE()
            for i,j in zip(range(len(lp_desc)),lp_parameter):
                lp_details[j] = lp_desc[i].text.strip().strip("\t").strip("\xa0").strip("\n")\
                    .strip("[查看详情]").strip("[查看地图]").strip("[房贷计算器]").replace(' ','')\
                    .strip("\n").strip("[价格走势")

            lp_namesp = lp_details["楼盘名称"].split()
            lp_details["楼盘名称"] = lp_namesp[0]
            lp_details["楼盘状态"] = lp_namesp[1]
            lp_price = re.sub("\D", '', lp_details["参考单价"])[0:5]
            lp_details["参考单价"] = lp_price

            for k,v in lp_details.items():
                lp_details[k] = v.replace('\xa0',' ').replace('\n',' ').replace('\r',' ')

            meDB.meCursor.execute('''INSERT INTO NEWPRERTYINFO_CDAJK_001 %s VALUES %s '''%(tuple(lp_details.keys()),tuple(lp_details.values())))
            #meDB.conn.close()

            time.sleep(1)

            #yield lp_details
```

* 下为创建数据库并建表的文件，保存在loupaninfo/public目录下的meSqlite .py文件中:

```py
# -*- coding: utf-8 -*-

__author__ = 'messageoom'

import time
import datetime
import sqlite3

class meDB(object):

    conn = sqlite3.connect('CDLPINFO_AJK.db')
    meCursor = conn.cursor()
    def crtTABLE(self):
        try:
            self.meCursor.execute('''CREATE TABLE IF NOT EXISTS NEWPRERTYINFO_CDAJK_001
            (id            INTEGER  PRIMARY KEY autoincrement,
            楼盘名称       TEXT,
            楼盘状态       TXET,
            楼盘特点       TEXT,
            楼盘类型       TEXT,
            参考单价       INT,
            最低首付       TXET,
            月供           TXET,
            楼盘总价       TXET,
            开间面积       TXET,
            商业面积       TXET,
            总建筑面积     TXET,
            招商业态       TXET,
            已签约商户     TXET,
            临近商圈       TXET,
            出售类型       TXET,
            周边人群       TXET,
            得房率         TXET,
            总套数         TXET,
            是否统一管理   TXET,
            是否分割       TXET,
            出租类型       TXET,
            租金           TXET,
            待租面积       TXET,
            待租套数       TXET,
            是否包含物业费  TXET,
            写字楼类型     TXET,
            写字楼级别     TXET,
            办公室面积     TXET,
            招租客群       TXET,
            已签约租户     TXET,
            临近CBD        TXET,
            公共部分精装修  TXET,
            标准层面积      TXET,
            物业类型       TEXT,
            开发商         TXET,
            区域位置       TXET,
            楼盘地址       TXET,
            售楼处电话     TXET,
            楼盘户型       TXET,
            最新开盘       TXET,
            交房时间       TXET,
            售楼处地址     TXET,
            建筑类型       TXET,
            产权年限       TEXT,
            容积率         TXET,
            绿化率         TXET,
            规划户数       TXET,
            楼层状况       TXET,
            工程进度       TXET,
            物业管理费     TXET,
            物业公司       TXET,
            预售许可证     TXET,
            车位数         TXET,
            车位比         TXET,
            楼盘图片       TXET,
            create_time   TIMESTAMP default (datetime('now', 'localtime')));''')

            self.conn.commit()
            #self.conn.close()
        except Exception:
            raise Exception
```

\*：_为了创建本地存储表花费了不少时间  ：}_

* 命令行进入loupaninfo目录 执行以下命令即可开始爬取

```bash
PS F:\scrips\loupaninfo> scrapy crawl loupaninfo
```



