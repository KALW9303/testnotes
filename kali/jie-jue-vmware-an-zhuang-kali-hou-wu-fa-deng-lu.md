# VMware安装Kali后无法登陆

> 最近看到群里大神些说Kali很强大，然后基于VMware虚拟化装了Kali，结果安装成功后竟然无法登陆，发现不是安装时自定义的用户名，而是root。故google了一把，找到了一个重置密码的方法，仅参考！

## 重置步骤

* #### 启动Kali Linux，等出现GRUB引导菜单时，选择“恢复模式”，按E键进入编辑模式。

### ![](/assets/grub01.png)

#### 进入编辑模式后参照下图进行修改（ro改为rw），添加init=/bin/bash

### ![](/assets/grub02.png)

* #### 编辑完成后按 Ctrl-X or F10继续启动

> 启动完成后，出现命令行，这时输入passwd root，回车就可以直接设置新密码（修改其他用户，把root改为其他用户名即可）

### 



