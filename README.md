# VPS一键搭建V2ray教程
## 准备工作
- 1、已经解析的域名，Win+R输入CMD 回车：键入ping 空格输入你的域名，检查一下是否可以ping通
- 2、一台境外VPS主流系统，例如：Debian/Ubuntu/CentOS
- 3、下载并安装FinalShell SSH工具

Windows版下载地址: http://www.hostbuf.com/downloads/finalshell_install.exe

macOS版下载地址: http://www.hostbuf.com/downloads/finalshell_install.pkg

 ### VPS服务器
Vultr注册链接：https://www.vultr.com/?ref=8941832-8H

VPS操作系统选择：Debian 10 x64


## V2Ray一键安装代码：


    bash <(curl -sL https://cdn.jsdelivr.net/gh/Misaka-blog/Xray-script@master/xray.sh)



## 放行端口
### Debian/Ubuntu  放行端口
例如要放行80端口

    iptables -I INPUT -p tcp --dport 80 -j ACCEPT

然后保存放行规则

    iptables-save



### Centos  放行端口
例如要放行80端口

    firewall-cmd --zone=public --add-port=80/tcp --permanent

然后重启防火墙

    firewall-cmd --reload

### 查看防火墙规则

    iptables -L
    
    
  
  
  # VPS中转教程
    获取root权限：
sudo -i


Ubuntu系统下：
开放所有端口
iptables -P INPUT ACCEPT
iptables -P FORWARD ACCEPT
iptables -P OUTPUT ACCEPT
iptables -F



国内机器
wget --no-check-certificate -qO natcfg.sh http://www.arloor.com/sh/iptablesUtils/natcfg.sh && bash natcfg.sh
国外机器
wget --no-check-certificate -qO natcfg.sh https://raw.githubusercontent.com/arloor/iptablesUtils/master/natcfg.sh && bash natcfg.sh



BBR 加速
wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh


防火墙解除
centos操作如下：
#停止firewall
systemctl stop firewalld.service
#禁止firewall开机启动
systemctl disable firewalld.service
#关闭iptables
service iptables stop
#去掉iptables开机启动
chkconfig iptables off

oracle Linux操作如下：
#停止firewall
systemctl stop firewalld.service
#禁止firewall开机启动
systemctl disable firewalld.service

ubuntu操作如下：
#Oracle自带的Ubuntu镜像默认设置了Iptable规则，关闭它
apt-get purge netfilter-persistent
reboot
#强制删除
rm -rf /etc/iptables && reboot



