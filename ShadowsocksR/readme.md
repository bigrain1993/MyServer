# 安装ShadowsocksR 服务端
## 一键脚本
### 安装
```
wget --no-check-certificate https://raw.githubusercontent.com/HMBSbige/MyServer/master/ShadowsocksR/shadowsocksR.sh && chmod +x shadowsocksR.sh && ./shadowsocksR.sh
```
### 编辑配置文件
```
vim /etc/shadowsocks.json
```
### 启动、停止、重启、查询状态
```
/etc/init.d/shadowsocks start/stop/restart/status
```
### 卸载
```
sh shadowsocksR.sh uninstall
```
### 开机自启动(一键脚本已自动加入)
#### CentOS/RHEL6 执行:
```
chmod 755 /etc/init.d/shadowsocks && chkconfig --add shadowsocks && service shadowsocks start
```
#### Ubuntu 14.x，Debian7.x 执行:
```
chmod 755 /etc/init.d/shadowsocks ; update-rc.d shadowsocks defaults ; service shadowsocks start
```
## 手动安装
### 安装所需
#### Centos
```
yum install git
yum install vim
yum install python-setuptools && easy_install pip
```
#### Ubuntu/Debian
```
apt-get install git
apt-get install vim
apt-get install python-pip
```

### 下载
```
git clone -b manyuser https://github.com/HMBSbige/shadowsocksr.git
```

### 初始化
```
cd ~/shadowsocksr
bash initcfg.sh
```
### 编辑配置文件

```
vim user-config.json
```

### 运行子目录内的server.py
```
cd ~/shadowsocksr/shadowsocks
python server.py
```
### 后台运行：
```
cd ~/shadowsocksr/shadowsocks
python server.py -d start
```
### 停止/重启：
```
python server.py -d stop/restart
```
### 查看日志：
```
tail -f /var/log/shadowsocks.log
```
### 更新源代码
#### 进入shadowsocksr目录
```
cd shadowsocksr
```
#### 执行
```
git pull
```
#### 成功后重启ssr服务
```
python server.py -d restart
```
# iptables防火墙简单配置
## 安装
```
apt-get install iptables
```
或
```
yum install iptables
```
## 清除已有iptables规则
```
iptables -F
iptables -X
iptables -Z
```
## 允许本地回环接口(即运行本机访问本机)
```
iptables -A INPUT -s 127.0.0.1 -d 127.0.0.1 -j ACCEPT
```
## 允许已建立的或相关连的通行
```
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
```
## 允许所有本机向外的访问
```
iptables -A OUTPUT -j ACCEPT
```
## 允许访问22端口
```
iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```
## 开机启动
```
chkconfig --level 345 iptables on
```
## 保存并重启
```
service iptables save
service iptables restart
```
# ShadowsocksR配置参数
## 加密
```
none
aes-256-cfb
aes-192-cfb
aes-128-cfb
aes-256-cfb8
aes-192-cfb8
aes-128-cfb8
aes-256-ctr
aes-192-ctr
aes-128-ctr
chacha20-ietf
chacha20
rc4-md5
rc4-md5-6
```
## 协议
```
origin
verify_deflate
auth_sha1_v4
auth_sha1_v4_compatible
auth_aes128_md5
auth_aes128_sha1
auth_chain_a
auth_chain_b
```
## 混淆
```
plain
http_simple
http_simple_compatible
http_post
http_post_compatible
tls1.2_ticket_auth
tls1.2_ticket_auth_compatible
tls1.2_ticket_fastauth
tls1.2_ticket_fastauth_compatible
```
