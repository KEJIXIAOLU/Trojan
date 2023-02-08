# 一键搭建Trojan-Go面板，配合使用CDN+Websocket，免费开启CDN隐藏自己VPS的真实IP，保护VPS永不被墙

### trojan多用户管理功能
- 在线web页面和命令行两种方式管理trojan多用户
- 启动 / 停止 / 重启 trojan 服务端
- 支持流量统计和流量限制
- 命令行模式管理, 支持命令补全
- 集成acme.sh证书申请
- 生成客户端配置文件
- 在线实时查看trojan日志
- 在线trojan和trojan-go随时切换
- 支持trojan://分享链接和二维码分享(仅限web页面)
- 支持转化为clash订阅地址并导入到clash_for_windows(仅限web页面)
- 限制用户使用期限

大神Jrohy的一键脚本支持Trojan-Go，相信在可靠性方面已经十分成熟。既然是一键脚本，我们只要有一台VPS，就可在上面很方便地安装部署。

## 准备工作
1、VPS一台重置好主流的操作系统（例：Debian10 64）

2、域名一个（已经解析的域名，Win+R输入CMD 回车：键入ping 空格输入你的域名，检查一下是否可以ping通）
（如果要使用Trojan-Go开启CND隐藏IP功能，需要将域名托管到CDN）

3、下载并安装FinalShell SSH工具

Windows版下载地址: http://www.hostbuf.com/downloads/finalshell_install.exe

macOS版下载地址: http://www.hostbuf.com/downloads/finalshell_install.pkg

## 搭建Trojan-go面板

### 开启Debian10自带的BBR加速
脚本如下，可以一起复制运行，或分四行代码一条一条运行。

    echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf
       
    echo "net.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.conf
    
    sysctl -p
    
    lsmod | grep bbr
    
## 更新系统安装环境

1、Debian/Ubuntu系统执行以下命令：。

    apt update -y && apt install -y curl
    
    
2、CentOS系统执行以下命令：

    yum update -y && yum install -y curl 
    
## Jrohy的一键Trojan面板脚本
### #安装/更新

    source <(curl -sL https://git.io/trojan-install)
    
### #卸载

    source <(curl -sL https://git.io/trojan-install) --remove
    
    
### 安装过程中，会出现3次提示，请根据以下选项进行：

- 1、第一次需要选择1. Let’s Encrypt证书
   请输入申请证书的域名：host.kjxlu.com
   
- 2、选择‘1. 安装docker版mysql’
   回车或手动输入用户名
   
注：跑完以上代码后，最后会出现一个选择菜单，不用理会，直接回车退出即可，即回到#提示符的状态下。至此，Trojan-Go面板搭建完成。

    
### 安装完后输入'trojan'可进入管理程序

浏览器访问 https://域名，可在线web页面管理trojan用户

第一次登陆面板时，会让您输入登陆密码，输入完后请使用用户名‘admin’及您设置的密码登陆。

-----------------------------------

## Trojan-Go 设置

### 登陆面板，修改Trojan类型为Trojan-Go

## 更改Trojan-Go配置文件
找到VPS目录文件 /usr/local/etc/trojan/config.json ，备份一份（若是把类型切换回来可以恢复使用Trojan）。

对着config.json文件按鼠标右键，选择‘用记事本编辑’。

- 注意：要在mysql的大括号}后加一个英文的逗号。路径和域名需要在客户端匹配。

         "websocket": {
        "enabled": true,
        "path": "/DFE4545DFDED/",
        "host": "你的域名"
       },
        "mux": {
        "enabled": true,
        "concurrency": 8,
        "idle_timeout": 60
        }

### 更改配置参数：
1、/DFE4545DFDED/为路径，随意填写。
2、host后 填上你的域名

### 保存后，在Trojan-Go面板重启服务。

## 下载Trojan-Go客户端
Trojan-QT5 （支持WIN/MACOS）
因为此Trojan-QT5 项目已经停更，所以只有1.4.0版本的供大家下载。
https://github.com/V2RaySSR/Trojan_panel_web/releases/tag/trojanqt5

- 如果Windows安装出错，请下载右面的附件： Trojan-Qt5-Windows 压缩包



