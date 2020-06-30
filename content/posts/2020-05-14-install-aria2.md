---
title: "linux 下安装 aria2 及自动上传到 OneDrive"
comment:
  enable: true
date: 2020-05-14T15:19:15+08:00
categories: ["技术"]
tags: ["aria2","OneDrive"]
featuredImagePreview: "https://cdn.jsdelivr.net/gh/Lucas-0/Img/img/20200630184152.jpg"
toc: 
lastmod: 2020-05-14T15:19:15+08:00
summary: "在 ECS 使用 aria2 下载与没有公网 IP 的 PC 相比有一定优势，但是 Lucas 所用的阿里云的小水管下载有 100 MB ，上传只有 1 MB，取回下好的东西还要漫长的等待。本文即为解决这一问题而写。"
---

---

</br>

**更新：**[https://github.com/uselibrary/Aria2Drive](https://github.com/uselibrary/Aria2Drive)

</br>

---

在 ECS 使用 aria2 下载与没有公网 IP 的 PC 相比有一定优势，但是 Lucas 所用的阿里云的小水管下载有 100 MB ，上传只有 1 MB，取回下好的东西还要漫长的等待。本文即为解决这一问题而写。

需要：<mark> OneDrive 账号</mark>

本文的系统为 `Ubuntu 18.04.4` 。

参考了下面的链接：

[PyOne使用文档--ShowDoc](https://www.showdoc.cc/pyone?page_id=2564166102352569)

[一个好用的OneDrive网盘上传工具，支持文件和文件夹上传](https://www.moerats.com/archives/1006/)

[使用Aira2下载文件后自动上传到Google Drive网盘](https://www.moerats.com/archives/482/)

&nbsp;&nbsp;


&nbsp;&nbsp;

## 安装 aria2  ##

推荐在宝塔下进行操作。[➡前往宝塔](https://www.bt.cn/)

### 1. 下载解压  aria2  ###

请检查链接是否为最新版，[GitHub项目地址](https://github.com/aria2/aria2)
```bash
wget -N --no-check-certificate https://github.com/aria2/aria2/releases/download/release-1.35.0/aria2-1.35.0.tar.gz
tar zxvf aria2-1.35.0.tar.gz
rm -rf aria2-1.35.0.tar.gz
cd aria2-1.35.0
make install
cd ..
rm -rf aria2-1.35.0
```

上面做的事情：下载➡解压➡删除压缩包➡进入解压的文件夹➡运行安装➡回到上一层文件夹➡删除解压的文件夹。

阿里云的 ECS 连接 GitHub 很慢，推荐下载到电脑上，利用宝塔手动上传，到哪个文件夹不重要，最终都会删掉。

### 2. 检查是否安装成功 ###

```bash
command -v aria2c
```

如果显示

```bash
/usr/bin/aria2c
```

  说明安装成功。

### 3. 下载 aria2 配置 ###

```bash
mkdir "/root/.aria2" && mkdir /root/Download
wget -N --no-check-certificate https://lucasdrive.imfast.io/Program/aria2/dht.dat -P '/root/.aria2/'
wget -N --no-check-certificate https://lucasdrive.imfast.io/Program/aria2/aria2.conf -P '/root/.aria2/'
wget -N --no-check-certificate https://lucasdrive.imfast.io/Program/aria2/trackers-list-aria2.sh -P '/root/.aria2/'
touch /root/.aria2/aria2.session
chmod +x /root/.aria2/trackers-list-aria2.sh
chmod 777 /root/.aria2/aria2.session  
```

  上面的链接可能会失效，届时配置文件也可按照其他教程设置。

### 4. 配置 aria2RPC 密钥  ###

修改文件 `/root/.aria2/aria2.conf` ，找到 `rpc-secret` ，然后给 `rpc-secret` 设置密码，作为密钥。

✅：注意要在宝塔面板中将 `aria2` 监听的端口放行，以及（如果有）安全组规则放行，否则 `aria2` 的速度会受到很大影响。

---

&nbsp;&nbsp;

## 设置开机启动 ##

创建 `/etc/systemd/system/aria2.service` ，不习惯 `vim` 可以直接在宝塔中新建文件，内容为：

```bash
[Unit]
Description=Aria2 server
After=network.target
Wants=network.target
[Service]
Type=simple
PIDFile=/var/run/aria2c.pid
ExecStart=/usr/bin/aria2c --conf-path=/root/.aria2/aria2.conf
RestartPreventExitStatus=23
Restart=always
User=root
[Install]
WantedBy=multi-user.target
```

然后 <kbd>esc</kbd> 、 <kbd>:wq</kbd> 退出保存，执行命令：

```bash
systemctl enable aria2
systemctl start aria2
```

此时 aria2 已经启动。

---

&nbsp;&nbsp;

## OneDrive上传控件 ##

点击右侧 `URL` 登录 OneDrive 并授权，授权地址→【[国际版、个人版(家庭版)](https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=78d4dc35-7e46-42c6-9023-2d39314433a5&response_type=code&redirect_uri=http://localhost/onedrive-login&response_mode=query&scope=offline_access%20User.Read%20Files.ReadWrite.All)】、【[世纪互联](https://login.chinacloudapi.cn/common/oauth2/v2.0/authorize?client_id=dfe36e60-6133-48cf-869f-4d15b8354769&response_type=code&redirect_uri=http://localhost/onedrive-login&response_mode=query&scope=offline_access%20User.Read%20Files.ReadWrite.All)】。

授权后会获取一个 `localhost` 开头打不开的链接，这里复制好整个链接地址，包括 `localhost` 。

### 1. 安装OneDriveUploader ###

```bash
#64位系统下载
wget https://raw.githubusercontent.com/MoeClub/OneList/master/OneDriveUploader/amd64/linux/OneDriveUploader -P /usr/local/bin/
#32位系统下载
wget https://raw.githubusercontent.com/MoeClub/OneList/master/OneDriveUploader/i386/linux/OneDriveUploader -P /usr/local/bin/
#arm架构下载
wget https://raw.githubusercontent.com/MoeClub/OneList/master/OneDriveUploader/arm/linux/OneDriveUploader -P /usr/local/bin/

#给予权限
chmod +x /usr/local/bin/OneDriveUploader
```

### 2. 初始化配置 ###

```bash
#国际版，将url换成你上面复制的授权地址，包括http://loaclhost。
OneDriveUploader -a "url"

#个人版(家庭版)，将url换成你上面复制的授权地址，包括http://loaclhost。
OneDriveUploader -ms -a "url"

#中国版(世纪互联)，将url换成你上面复制的授权地址，包括http://loaclhost。
OneDriveUploader -cn -a "url"
```

如果提示 `Init config file: /root/auth.json` 类似信息，则初始化成功。

### 3. 使用命令 ###

```bash
Usage of OneDriveUploader:
  -a string
        // 初始化授权
        Setup and Init auth.json.
  -b string
        // 自定义上传分块大小, 可以提高网络吞吐量, 受限于磁盘性能和网络速度.
        Set block size. [Unit: M; 5<=b<=60;] (default "10")
  -c string
        // 配置文件路径
        Config file. (default "auth.json")
  -n string
        // 上传单个文件时,在网盘中重命名
        Rename file on upload to remote.
  -r string
        // 上传到网盘中的某个目录, 默认: 根目录
        Upload to reomte path.
  -s string
        // *必要参数, 要上传的文件或文件夹
        Upload item.
  -t string
        // 线程数, 同时上传文件的个数. 默认: 2
        Set thread num. (default "2")
  -f
        // 开关(推荐)
        // 加上 -f 参数，强制读取 auth.json 中的块大小配置和多线程配置.
        // 不加 -f 参数, 每次覆盖保存当前使用参数到 auth.json 配置文件中.
        Force Read config form config file. [BlockSize, ThreadNum]
  -skip
        // 开关
        // 跳过上传网盘中已存在的同名文件. (默认不跳过)
        Skip exist file on remote.
  -cn
        // 开关
        // 授权中国版(世纪互联), 需要此参数.
        OneDrive by 21Vianet.
  -ms
        // 开关
        // 授权个人版(家庭版), 需要此参数.
        OneDrive by Microsoft.
```

### 4. 命令示例 ###

```bash
#将当前目录下的mm00.jpg文件上传到OneDrive网盘根目录
OneDriveUploader -c /path/to/file/auth.json -s "mm00.jpg"

#将当前目录下的mm00.jpg文件上传到OneDrive网盘根目录，并改名为mm01.jpg
OneDriveUploader -c /path/to/file/auth.json -s "mm00.jpg" -n "mm01.jpg"

#将当前目录下的Download文件夹上传到OneDrive网盘根目录
OneDriveUploader -c /path/to/file/auth.json -s "Download" 

#将当前目录下的Download文件夹上传到OneDrive网盘Test目录中
OneDriveUploader -c /path/to/file/auth.json -s "Download" -r "Test"

#将同目录下的Download文件夹上传到OneDriv网盘Test目录中，使用10线程
OneDriveUploader -c /path/to/file/auth.json -t 10 -s "Download" -r "Test"

#将同目录下的Download文件夹上传到OneDrive网盘Test目录中，使用15线程，并设置分块大小为20M
OneDriveUploader -c /path/to/file/auth.json -t 15 -b 20 -s "Download" -r "Test"
```

---

&nbsp;&nbsp;

## aria2 自动上传 ##

### 1. aria2 自动上传脚本 ###

上传脚本代码如下：

```sh
#!/bin/bash

GID="$1";
FileNum="$2";
File="$3";
MaxSize="15728640";
Thread="3";  #默认3线程，自行修改，服务器配置不好的话，不建议太多
Block="5";  #默认分块5m，自行修改
RemoteDIR="";  #上传到Onedrive的路径，默认为根目录，如果要上传到MOERATS目录，""里面请填成MOERATS
LocalDIR="/www/download/";  #Aria2下载目录，记得最后面加上/
Uploader="/usr/local/bin/OneDriveUploader";  #上传的程序完整路径，默认为本文安装的目录
Config="/root/auth.json";  #初始化生成的配置auth.json绝对路径，参考第3步骤生成的路径


if [[ -z $(echo "$FileNum" |grep -o '[0-9]*' |head -n1) ]]; then FileNum='0'; fi
if [[ "$FileNum" -le '0' ]]; then exit 0; fi
if [[ "$#" != '3' ]]; then exit 0; fi

function LoadFile(){
  if [[ ! -e "${Uploader}" ]]; then return; fi
  IFS_BAK=$IFS
  IFS=$'\n'
  tmpFile="$(echo "${File/#$LocalDIR}" |cut -f1 -d'/')"
  FileLoad="${LocalDIR}${tmpFile}"
  if [[ ! -e "${FileLoad}" ]]; then return; fi
  ItemSize=$(du -s "${FileLoad}" |cut -f1 |grep -o '[0-9]*' |head -n1)
  if [[ -z "$ItemSize" ]]; then return; fi
  if [[ "$ItemSize" -ge "$MaxSize" ]]; then
    echo -ne "\033[33m${FileLoad} \033[0mtoo large to spik.\n";
    return;
  fi
  ${Uploader} -c "${Config}" -t "${Thread}" -b "${Block}" -s "${FileLoad}" -r "${RemoteDIR}" -skip
  if [[ $? == '0' ]]; then
    rm -rf "${FileLoad}";
  fi
  IFS=$IFS_BAK
}
LoadFile;
```

编辑好上传脚本后，可以检测下脚本编码是否正确，比如我脚本路径为 `/root/upload.sh` ，使用命令：

```bash
bash /root/upload.sh
```

如果无任何输出，则正确，反之输出类似 `$'r': command not found` 错误，则需要转换下编码格式，具体步骤如下。

先安装 `dos2unix` ：

```bash
#CentOS系统
yum install dos2unix -y

#Debian/Ubuntu系统
apt install dos2unix -y
```

再转换编码：

```bash
#后面为脚本路径
dos2unix /root/upload.sh
```

### 2. 下载完成后执行 ###

设置下载完成自动上传，传输后删除服务器上的文件：

```bash
#授权
chmod +x /root/upload.sh
```

然后到 `aria2` 配置文件中加上一行：

`on-download-complete=/root/upload.sh`

即可，后面为脚本的路径。

最后重启 `aria2` 生效。

```bash
systemctl restart aria2
```

---

&nbsp;&nbsp;

至此，当 aria2 中的下载任务完成后会自动将文件上传到 OneDrive ，之后可以利用 IDM 下载到本地，实现吃灰小鸡再就业。

PS：几个指令：

1. 使用 `clear` 命令或 `reset` 命令清空当前屏幕，or
清空屏幕快捷键：

```bash
ctrl + l
```

2. 清空当前输入快捷键：

```bash
   ctrl + u
```

3. 放弃当前输入快捷键：

```bash
   ctrl + z
```

&nbsp;&nbsp;

&nbsp;&nbsp;

