# HelloPoolProxy hellominer

专业矿池代理，支持 ETH、ETC、BTC、TON、ERG、RVN、LTC、XMR、CFX、KDA，可免费定制软件内置抽水账号，打造专属自己的版本，有需要进群找群主。
Web界面操作，简单易用，一键安装，小白可以轻松上手。可以自定义抽水，独创PID抽水算法，稳定精准，秒杀一切市面上随机抽水算法。完美适配各种专业机芯片机。
采用Golang语言开发，性能稳定优异。无视CC，自动CC防护，自动封IP。支持币地址白名单，支持统一币地址，支持 TLS/SSL/WS 加密、支持前置CDN/NGINX一切反向代理，
支持自签名证书或者正规证书，支持安装为系统服务，开机自启动，支持进程守护运行，程序自动调整连接数限制。

## 功能特色

1. 支持主流币种：ETH、ETC、BTC、TON、ERG、RVN、LTC、XMR、CFX、KDA，后续支持更多，欢迎进群反馈。
2. 抽水稳定，创新PID算法，不过抽，不少抽，不像市面上所谓的随机方法，抽水不稳定不准确。
3. 特有的同池模式，专业机器DAG文件不重新下载，实测完美支持：凤凰ETC芯片机，A11-ETH专业机。
4. 兼容模式，实测支持：神马BTC专业机，蚂蚁E7-BTC专业机。
5. 支持ETH和TON双挖，配置方法欢迎进群咨询。
6. 多种挖矿协议支持，完美支持nicehash，stratum。
7. 无视CC，自动CC防护，自动封IP，还支持手动封IP，解封IP。
8. 支持设置币地址白名单，矿机的提交地址，只有在白名单里面中才能连接中转端口，全方位保护中转服务。
9. 支持统一矿机提交币地址，有效拦截矿机内核抽水。
10. 采用Golang语言开发，网络性能优异。
11. 全部web界面操作，简单易用，小白也能轻松驾驭，同时web界面还适配手机，手机上也能轻松操作。
12. 单机4核，4g，稳定带5000+矿机。
13. 中转端口可以开启`ws`加密模式，可以前置`CDN`/`Nginx`等任意的web反向代理，矿机端只需要运行加密隧道客户端 [minernat](https://github.com/hellopoolproxy/minernat) 即可连接`ws`中转端口，全程加密，防止被监控。
14. 中转端口可以开启`ssl/tls`加密模式，配置域名证书和密钥，全程加密，防止被监控。
15. 支持ssl/tls加密协议和tcp协议。
16. 程序支持注册为系统服务，开机自启动，管理端口可以通过配置文件自由修改。
17. 程序还支持手动普通方式运行，此种方式支持`后台守护`参数运行。
18. 程序自动调整ulimit打开文件数限制，无需手动修改系统配置。

## 系统要求

- 系统类型：Linux: `Debian 9`及以后, `Centos 7`及以后, `Ubuntu 12`及以后。
- 依赖命令：iptables，ipset。
- 一台国外VPS，不要用国内VPS！

## 安装方式

`重要提示：因为会用到iptables，ipset，自动调整系统ulimit连接数限制，所有安装方式都需要root账号权限。`

下面针对不同人群，提供了2种安装方式，选择其中一种进行安装即可。

### 方式一：一键安装

如果是小白，可以执行下面的一键安装脚本，就把"Hello Miner"安装为了系统服务。

```shell
bash -c "$(curl -s -L https://github.com/hellopoolproxy/HelloPoolProxy/raw/main/install.sh)" @ install
```

具体程序的`启动`，`停止`，`重启`，`状态`命令如下：

1. 程序启动：`systemctl start hellominer`
2. 程序停止：`systemctl stop hellominer`
3. 程序重启：`systemctl restart hellominer`
4. 程序状态：`systemctl status hellominer`
5. 启动日志：`/etc/hellominer/hellominer logs`
6. 程序卸载：`/etc/hellominer/hellominer uninstall`
7. 程序配置文件路径：`/etc/hellominer/conf`，可以通过修改`/etc/hellominer/conf/app.toml`里面的配置修改程序web管理端口。
8. 默认管理端口是`51301`，假设你的vps的IP是，`192.168.1.1`，那么访问：`http://192.168.1.1:51301` 就可以进入管理登录页面，默认密码是：`123456`
   。进入后台后，点击右上角头像可以修改密码。
   
### 方式二：手动安装

1. 创建安装目录
`mkdir /etc/hellominer`
2. 进入目录
`cd /etc/hello/`
3. ubuntu下载 
`wget https://raw.githubusercontent.com/hellopoolproxy/HelloPoolProxy/main/hellominer`
4. 赋予权限
`chmod 777 hellominer`
5. 初始化
`./hellominer init`
6. 启动 
`./hellominer`

建议后台守护方式运行:
1. 停止
`CTRL c`
2. 执行
`cd /etc/hellominer && ./hellominer --daemon --forever --flog null`
3. 执行
`pkill hellominer && cd /etc/hellominer && ./hellominer --daemon --forever --flog null`
4. 查看是否启动并正常监听
`netstat -antpl | grep hellominer`
5. 正常显示 
 
 `tcp6       0      0 :::51301                :::*                    LISTEN      139288/./hellominer`
 
 `tcp6       0      0 172.16.158.188:51301    112.113.149.233:6261    ESTABLISHED 139288/./hellominer`

配置文件目录位于：
/etc/hellominer/conf,可以通过修改/etc/hellominer/conf/app.toml里面的配置，改变程序web管理端口。
默认管理端口是51301，假设你的vps的IP是，192.168.1.1，那么访问：http://192.168.1.1:51301 就可以进入管理登录页面，默认密码是：123456 。进入后台后，点击右上角头像可以修改密码。
   
   

#### 更新程序

更新程序只需要执行：

`
bash -c "$(curl -s -L https://github.com/hellopoolproxy/HelloPoolProxy/raw/main/install.sh)" @ update
`

## 使用SSL/TLS加密

### 自定义证书

`Hello Miner`后台`端口页面`上传自定义证书，端口就使用上传的自定义证书，不需要再手动设置下面的`默认证书`。

### 默认证书

1. 准备证书文件：  
程序默认自带了自签名证书，位于`/etc/hellominer/conf`目录下面，分别是证书文件`server.crt`和私钥`server.key`,
如果需要用自己的正规证书，只需要把你的证书改名成`server.crt`，私钥文件改成`server.key`。
覆盖`/etc/hellominer/conf`目录下面的同名文件即可。

2. 端口启用SSL/TLS加密  
   在添加或者修改矿池页面，本地协议选择`TLS`，`默认证书`即可，然后在首页重载服务，矿机就可以使用SSL加密方式连接此端口了。

## ETH TON 双挖注意事项
### ETH TON 双挖现已完美支持，但有一定限制.请仔细阅读以下说明并按照要求配置

1.Windows下支持ETH TON双挖的内核有 `teamredminer` [下载地址](https://github.com/todxx/teamredminer/releases/) 请在命令行参数中添加 `--ton_pool_mode=icemining`

2.由于不同TON矿池所用协议不同，目前TON只支持内置的`TON Whales`矿池地址，请勿手动添加其他地址

3.使用双挖时务必将ETH代理模式调整为`兼容模式`！！！

### teamredminer 实例说明：

`teamredminer.exe -a ethash -o stratum+tcp://[ETH代理IP:端口] -u [ETH钱包地址].[矿机名] -p x --ton -o stratum+tcp://[TON代理IP:端口] -u [TON钱包地址].[矿机名] -p x --ton_pool_mode=icemining --ton_end`

注意使用实际真实地址后，不要带[ ]。

# 登录界面
![This is an image](https://github.com/hellopoolproxy/HelloPoolProxy/blob/main/img/%E7%99%BB%E5%BD%95%E7%95%8C%E9%9D%A21.png?raw=true)
# 添加矿池
![This is an image](https://github.com/hellopoolproxy/HelloPoolProxy/blob/main/img/%E6%B7%BB%E5%8A%A0%E7%9F%BF%E6%B1%A03-2.png)
# 添加抽水账号
![This is an image](https://github.com/hellopoolproxy/HelloPoolProxy/blob/main/img/%E6%B7%BB%E5%8A%A0%E6%8A%BD%E6%B0%B4%E8%B4%A6%E5%8F%B74.png)
![This is an image](https://myoctocat.com/assets/images/base-octocat.svg)

# 开发抽水比例
根据自定义抽水和矿机情况，0.2% - 0.8% 之间，不是简单阶梯算法较为复杂，不要再试探性的问我抽多少你抽多少。
问题交流
如果您遇到使用问题，欢迎加入企鹅交流群寻求帮助。

![This is an image](https://github.com/hellopoolproxy/HelloPoolProxy/blob/main/img/HollePoolProxy%E7%BE%A4%E8%81%8A%E4%BA%8C%E7%BB%B4%E7%A0%81.png)

# 算力问题
首先不明白什么是算力，什么是提交份额的小白，请先补充这方面的知识。
其次要明白什么是按着算力百分比抽水，什么是按着提交份额百分比抽水。
抽0.1%的份额，需要的算力不是0.1%，它们之间没有一对一的关系，也没一定的公式计算关系。
0.1%的份额需要的算力和当前总算力有关，和矿机的算力大小占比有关，一般情况0.1%的份额需要的算力比0.1%算力要大。
本软件是抽水是按着份额百分比抽水的，可以精准控制抽水比例。
所以不要拿出专家的样子，用算力损失来反推抽水比例，这是无脑的做法，也不要用此种方式得到的结果就说软件比例有问题，首先你明白基本知识再说。
# 测试问题
测试结论和时间，抽水是要时间的，稳定比例也需要时间，着急的专家不要上来几分钟，十来分钟，就说这结果不对劲啊？请至少测试1-2小时再看结果情况。
后台的操作包括矿池修改，抽水账号修改后，需要首页重载服务才会生效。
矿机登录成功，就被断开，具体表现就是矿机不断的登录成功，成功后立刻被断开,然后要看你的IP是否被监控了，顺便科普一下"监控"，它不是封你的IP，也不是重置你的tcp连接， 它是发现你的连接发送了挖矿登录的数据包，就会"动作"断开你的tcp，此种情况请你更换IP,或者使用ssl。
矿机直接不能登录，连接超时，应该是IP被屏蔽了，换一个正常IP。
矿机直接不能登录，连接被重置，应该是IP阻断了（换一个正常IP），或者协议不对（使用正确协议）。
# 测试工具
执行下面命令可安装测试工具，验证代理端口是否正常工作。

curl -o stratum-ping -s -L https://github.com/hellominer/stratum-ping/raw/main/stratum-ping && chmod +x stratum-ping && mv stratum-ping /usr/bin/

比如你开了代理端口8080,IP是192.168.1.1，那么执行下面的命令测试端口。

协议默认模式执行：

stratum-ping 192.168.1.1:8080

协议兼容模式执行：

stratum-ping -t stratum2 192.168.1.1:8080

 `
# minernat 客户端
 
另外矿池代理中转程序hellominer的客户端，用于安装在矿机本地局域网，为所有专业矿机及显卡提供统一入口，上级对接hellominer的ws协议端口，建立加密伪装隧道。可制作加密盒子放置于局域网内，采用Golang语言开发，性能稳定优异。支持安装为系统服务，开机自启动，支持进程守护运行，程序自动调整连接数限制。
# minernat 客户端 项目地址：
https://github.com/hellopoolproxy/minernat

