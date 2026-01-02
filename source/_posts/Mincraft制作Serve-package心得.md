---
title: Minecraft 制作 Serve-package 心得
date: 2025-12-30 10:00:00
tags:
  - Minecraft
  - 服务器
categories:
  - 教程
description: 自己制作Minecraft服务端
cover: ''
---
开服务器和朋友玩整合包时，会遇到有些整合包只有客户端没有服务端的情况，这时候就需要我们自己去制作服务端，下面以记录了一次开服经历，方便之后查看。

<!-- more -->

# 总览  
服务端：**Forge**   
联机方式：**樱花Frp** 

# 1 环境准备  
## 1.1 硬件准备   
- 至少 4 GB 的 RAM
- 至少 50 GB 的硬盘空间
- 较大上传带宽   
## 1.2 软件准备  
### 1.2.1 JAVA   
#### (1) JAVA版本
&emsp;&emsp;不同整合包使用，Minecraft游戏版本不同，所需要的 Java 版本也不同。部分整合包的下载处会告知使用的java的版本，如果找不到，自行通过其他方式查询。   
&emsp;&emsp;以下是网上博主总结的对应关系，仅作参考：   
| 游戏版本 | JAVA版本 |
| :----: | :----: |
| <= 1.12.2 | JAVA 8 |
| 1.16.5 | JAVA 11 |
| >= 1.17 | JAVA 17 |       

&emsp;&emsp;下面是本人玩整合包以来，下载过的JAVA版本，仅作参考：    
| JAVA版本 |
| :----: |
| JDK 1.8.0_381 |
| JDK 11.0.13 |
| JDK 17.0.12 |
| JDK 18.0.2.1 |
| JDK 21.0.8 |    
#### (2) JAVA下载   
&emsp;&emsp;来到此网址：[Java 版本发布历史](https://www.java.com/releases/)，可以获取广泛发布的 Java SE 版本以及指向每个版本关键信息的链接，找到对应的版本进行下载安装即可。    
![Java 版本发布历史](./Java%20版本发布历史.png "Java 版本发布历史")    

### 1.2.1 SakuraFrp   
- &emsp;来到此网址：[SakuraFrp官网](https://www.natfrp.com/)，注册账号后，下载客户端并进行登录。    
- &emsp;在网页端中，点击  **用户** --> **实名认证**
- &emsp;在网页端中，点击  **服务** --> **隧道列表** --> **创建隧道**，选择节点    
  - &emsp;可先点击  **服务** --> **节点状态**，查询在线节点
- &emsp;选择节点后，隧道类型选择 <font color=red>**TCP隧道**</font> ，隧道名任意输入，本地IP留空， **本地端口** 选择 <font color=red>**【25565】 Minecraft Java**</font>，然后点击创建即可。    
## 1.3 Forge 服务端   
### 1.3.1 下载Forge 服务端   
来到此网址：[Forge 服务端](https://files.minecraftforge.net/net/minecraftforge/forge/)下载对应 Minecraft 版本的安装包    
![Forge 服务端历史版本](./Forge%20服务端历史版本.png "Forge 服务端历史版本")     
若点击下载无响应，无法下载，在下载页面，右键 Installer 按钮，复制链接并粘贴网页栏里面，把 &url= 以及前面的所有字符都去掉，再回车访问页面即可开始下载      
- 下载到形如 **forge-xxx-xxx-installer.jar** 的安装包后，在终端中使用以下代码打开安装：    
```javascript {.line-numbers}
java -jar "安装包文件名.jar"   
```
- 点击 `Install Serve`,选择要存放服务器文件的文件夹路径，等待安装完成即可    
### 1.3.2 配置Forge 服务端   
- 安装完成后，来到安装文件夹，将整合包中游戏的`jar`文件复制进来
- 将 **mod文件夹** ， **配置文件夹** 等都复制进来（但需要剔除掉服务端不能安装的mod）
  - 可以在浏览器搜索mod是否可以安装于服务端，适用于少量mod的整合包
  - 现在一般整合包mod都很多，可以先双击运行启动脚本，自行解读报错信息，或将报错信息复制给ChatGPT，让他分析报错信息，删除掉服务端不需要的mod
  - 如果不清楚要复制哪些文件夹，可以把除了 **saves** 之外的文件夹都复制过来
- 第一次双击启动脚本后，会生成`eula.txt`文件，用记事本打开后，最后一行改为：
```javascript {.line-numbers}
eula=true
```
- 然后再次双击启动脚本即可   

**至此服务器开启完成**   
## 1.4 联机
&emsp;&emsp;服务器开好后，打开 SakuraFrp 客户端，启动首页中创建的隧道，在日志中，找到 `IP : Port`的形式，发送给朋友即可