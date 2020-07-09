# 使用 colab 安装 rclone 以及搭建 gd_utils


<!--more-->
</br>
</br>
有很多患有仓鼠综合征的人喜欢到处收集, 把资源放在谷歌的共享盘中, 这类团队盘名义上不限制容量, 但是文件数量有 40w 的限制, 尽管并不是很严格的在执行. 用来放一些丢了也不心疼的内容不失为一个好方法.

其中有些人会把资源分享出来, 路人获取到资源的分享链接虽然可以查看文件, 然而有下载和播放等的流量限制, 短时间流量过大会触发保护. 由于现在团队盘很容易获取, 转存到自己的团队盘可以间接解决这一问题, 但是有每 24h 750GB 的限制. gd_utils 即是一个解决方案. 项目地址:

[https://github.com/iwestlin/gd-utils](https://github.com/iwestlin/gd-utils)

{{<admonition title="类似的项目">}}
[gclone](https://github.com/donwa/gclone)
{{</admonition>}}

原项目需要一个能连接谷歌服务的 VPS , 但是如果没有的话单纯为转存文件租一台并不合算. 借助谷歌的 colab 平台, 可以实现核心功能 ( 而且分配的虚拟机性能秒杀你能租到的 VPS, 毕竟是给机器学习用的 ). 至于 Telegram 的 bot 我并不感兴趣, 所以没有考虑.
    
</br>

---

## 创建应用申请 token (optional)

**选做但推荐.**

根据下面教程申请 API, 创建应用并获取 `client_id` 和 `client_secret`, 然后进入 [colab](https://colab.research.google.com) 平台.

[GoIndex：一个无需服务器的Google Drive目录索引程序 - Rat's Blog](https://www.moerats.com/archives/1001/)

遇到的验证参照下面的链接解决:

[Rclone高级玩法--利用服务账号突破日流量750G限制 - Jialezi `s blog](http://blog.jialezi.net/?post=153)

创建 notebook , 只需要将普通的 bash 命令前加上 `!` 即可执行. 如下:

</br>

```bash
# 安装依赖
!apt update && apt install curl unzip -y

# 安装 rclone
!curl https://rclone.org/install.sh | sudo bash

# 配置 conf 文件获取 refresh_token, 具体操作有很多写的极为详细的教程
!rclone config
```

然后可以复制输出信息或者下载 rclone.conf 文件, 里面有所需要的全部信息.

</br>

## 创建项目获取 service account

截至目前网络上所有创建 service account 的方案都是借助 AutoRclone 项目创建的.

项目地址: [https://github.com/xyou365/AutoRclone](https://github.com/xyou365/AutoRclone)

我在 VPS 上完成的这一步, 理论上在 colab 上也能实现. 可参照如下教程新建项目: 

[AutoRclone配合gclone突破GoogleTeamDrive750G流量限制 - Largesse's blog](https://largesse.12306.recipes/posts/e5e17474.html#%E5%AE%89%E8%A3%85%E8%AF%A6%E7%BB%86%E8%BF%87%E7%A8%8B)

[Use “AutoRclone + gclone” 教程 Copy GoogleDrive Resources Easy – FXXKR LAB](http://fxxkr.com/2020/03/27/autorclone-gclone-googledrive/)

[gclone配置教程 - Juch Blog](https://blog.juchiahau.com/2020/04/gclone-config.html)

<!--

```bash
# 升级源与安装必备的环境, 注意 colab 需要前缀 !
apt update -y &&　apt upgrade -y
apt install wget curl screen git sudo python3-distutils -y
sudo -i

# 安装 python3 & pip3
apt install python3 python3-pip -y

# 下载并安装 AutoRclone
cd ~
git clone https://github.com/xyou365/AutoRclone && cd AutoRclone && sudo pip3 install -r requirements.txt
```
-->

​    

运行下面的命令:

```
cd
cat ~/AutoRclone/accounts/*.json | grep "client_email" | awk '{print $2}'| tr -d ',"' | sed 'N;N;N;N;N;N;N;N;N;/^$/d;G' > ~/email.txt
```

在根目录下生成 email.txt 文件便于添加入 group.

推荐创建群组管理这些小号, 如要了解 Shared drive 的限制, 请看下面的官方解释[^1].

​    

## 搭建 gd_utils

colab 中执行代码块:
```bash
!curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
!apt-get install -y nodejs   # 安装node.js

!git clone https://github.com/iwestlin/gd-utils  # 下载gd-utils
%cd gd-utils

!npm install --unsafe-perm=true --allow-root  # 安装依赖
!apt install pm2
!npm i pm2 -g

# 然后把 service account 的 json 文件上传到 gd_utils 的 sa 目录下, config.js 修改参数后替换文件, colab 里可以直接双击打开修改保存. 这一步我建议预先把文件传到自己的谷歌硬盘, 运行时从谷歌硬盘复制    

!pm2 start server.js # 运行 server

!node check.js # 输出根目录则成功

!./validate-sa.js [target folder] # 检验 service account 是否都有搬运至目标文件夹的权限, [target folder] 为文件夹的 ID

!./copy -h # 查看帮助

!./backup-db.js  # 备份失败的任务进度, 下次可以断点续传
```

最常用的命令应该是在两个文件夹之间拷贝文件:

`./copy <source id> <target id> -S`

注意 `S` 是大写, 意为使用 service account.

搭建 gd_utils 和 gclone 的教程有很多, 所以我写的比较简略; 不过缝合了多个教程, 完全利用 colab 做到无服务器实现, 也算是一点创新之处吧.

一点说明:

根据 gd_utils 项目的作者所说, 谷歌硬盘在拷贝文件时并不是真的创建了一个副本, 而是增加了一个索引.

> 首先要明确一下 server side copy（后称ssc） 的原理。
>
> 对于 Google Drive 本身而言，它不会因为你ssc复制了一份文件而真的去在自己的文件系统上复制一遍（否则不管它有多大硬盘都会被填满），它只是在数据库里添上了一笔记录。

所以 Shared drive 之间互相拷贝大文件不会给谷歌的存储造成额外负担, 这一部分的负罪感可以放下. 

毕竟有薅羊毛之嫌疑, 请合理使用, 并做好随时失去的心理准备.

​    

题外话:

[一个谷歌硬盘的目录索引程序](https://github.com/Aicirou/goindex-theme-acrou)

​    

[^1]:[共享云端硬盘的限制](https://support.google.com/a/answer/7338880?hl=zh-Hans)
