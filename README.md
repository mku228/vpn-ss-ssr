# 2022一键脚本搭建SS个人VPN搭建SSR服务并开启BBR加速教程

本个人VPN搭建教程面向零基础小白，从 0 搭建属于自己的VPN服务实现科学上网，访问一线资源。

手把手教你搭建自己的shadowsocks/shadowsocksR代理服务器实现科学上网。可用翻墙方法，一键脚本，小白可以搭建。内容包括VPS购买，连接VPS，一键搭建shadowsocks/shadowsocksR，开启bbr加速，客户端配置shaodowsocks。

## 优惠购买云服务器vultr

在搭建之前需要一台境外的云服务器，而 [vultr](https://www.vultr.com/?ref=8944093-8H) 服务商比较稳定，安全，相当于境内的阿里云。

值得说的一点是， [vultr](https://www.vultr.com/?ref=8944093-8H) 给新用户的福利相当给力，充值 10 美元就可以获取 100 美元，你可以点击 [vultr 专属赠送新用户 100 美元](https://www.vultr.com/?ref=8944093-8H) 进去抢先注册。

右上角有注册按钮，你也可以切换成中文界面：

<img width="1446" alt="vpn搭建教程" src="https://user-images.githubusercontent.com/84239400/119019442-be0cc500-b98c-11eb-895b-0d6300dce93d.png">

![](https://user-images.githubusercontent.com/84239400/119019760-0d52f580-b98d-11eb-9837-aba0990f1dfb.png)

接着使用邮箱和密码就可以注册了。

![](https://user-images.githubusercontent.com/84239400/119020042-4ee3a080-b98d-11eb-8341-bfc30f4b103c.png)

进去之后你可以看到这个页面，说明你已经通过 [vultr 专属优惠链接](https://www.vultr.com/?ref=8872890-6G) 获得了 100 美元赠送的资格：

![](https://user-images.githubusercontent.com/84239400/119020173-733f7d00-b98d-11eb-8ecc-a1afeb556fe6.png)

现在你只要选择支付宝充值 10 美元以上，就可以获得额外赠送的 100 美元。

![](https://user-images.githubusercontent.com/84239400/119020280-966a2c80-b98d-11eb-9113-8f5f0b75c5ea.png)

接下来就可以在这个平台选购云服务器了。

点击页面左边菜单栏的 「Products」进入服务器选购页面。

### Choose Server 选择服务器

选择 Cloud Compute 即可：

![](https://user-images.githubusercontent.com/84239400/119020373-af72dd80-b98d-11eb-8478-02d735b82709.png)

### Server Location

服务器的位置，可以选择美国地区，比如纽约：

![](https://user-images.githubusercontent.com/84239400/119020467-cadde880-b98d-11eb-8927-d3d837bbc20c.png)

### Server Type

服务器类型，CentOS 8 x64 系统：

<img width="1297" alt="vpn搭建教程" src="https://user-images.githubusercontent.com/84239400/119020720-198b8280-b98e-11eb-9df3-19bf5a187a1e.png">

### Server Size

内存，个人使用10G完全够用，这里选择3.5美元一个月，性价比高，注意不要选择IPv6 ONLY的，要不然无法搭建使用。

<img width="1240" alt="vpn搭建教程" src="https://user-images.githubusercontent.com/84239400/119020895-4a6bb780-b98e-11eb-9ac8-3cdd4f4397de.png">

选择完了之后，下面的其它东西都不需要填，直接点击右下角 Deploy Now 就可以了：

![](https://user-images.githubusercontent.com/84239400/119020981-68391c80-b98e-11eb-9f16-00c75de88eeb.png)

这时候你就拥有了自己的一台云服务器了：

<img width="1261" alt="VPN搭建教程" src="https://user-images.githubusercontent.com/84239400/119021075-86068180-b98e-11eb-82a9-71edb9934f23.png">


点击 Cloud Instance ，可以看到你服务器的 IP 地址和密码：

<img width="1308" alt="vpn搭建教程" src="https://user-images.githubusercontent.com/84239400/119021183-a20a2300-b98e-11eb-8ff4-7f18d3e3bb80.png">

## 连接到你的服务器

### windows 系统连接到 vultr 服务器

windows 可以下载[PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)工具。

打开之后选择 session，将你在 vultr 网上得到的服务器 ip 复制过来，输入到这里：

![](https://user-images.githubusercontent.com/84239400/119023900-037fc100-b992-11eb-85ea-525a61a69657.png)

Port 默认 22，Connection Type 选择 SSH，接着点击 Open，连接进去之后输入你云服务器的密码。

### Linux 和 MacOS 连接到 vultr 服务器

Linux 和 MacOS 可以打开终端，使用如下命令连接：

```
ssh root@xx.xx.xxx.xx
```

`xx.xx.xxx.xx`就是你的服务器上的 IP 地址。

连接进去之后输入 yes 后按回车，接着输入你云服务器的密码，即可使用云服务器。

<img width="772" alt="vpn搭建教程" src="https://user-images.githubusercontent.com/84239400/119024049-32963280-b992-11eb-8c05-db6df1f7fbfa.png">

# 一键搭建shaodowsocks/shadowsocksR

注意，shadowsocks/shadowsocksR这两个只需要搭建一个就可以了！！！！SS与SSR之间的比较一直是各有各的说法，王婆卖瓜自卖自夸。我用的是SS，因为SS的iOS版本比较容易下载，并且被没有觉得ss容易被探查到~

## 一键搭建shadowsocks

1.下载一键搭建ss脚本文件（直接复制这段代码运行即可）

git clone -b master https://github.com/flyzy2005/ss-fly

![image](https://user-images.githubusercontent.com/98797623/152299551-a189f370-3548-42ad-b015-c3765f610397.png)

2.运行搭建ss脚本代码

ss-fly/ss-fly.sh -i 你的密码 1024
其中【你的密码】换成你要设置的shadowsocks的密码即可（这个【你的密码】就是你ss的密码了，是需要填在客户端的密码那一栏的），密码随便设置，最好只包含字母+数字，一些特殊字符可能会导致冲突。而第二个参数1024是端口号，也可以不加，不加默认是1024~（举个例子，脚本命令可以是ss-fly/ss-fly.sh -i qwerasd，也可以是ss-fly/ss-fly.sh -i qwerasd 8585，后者指定了服务器端口为8585，前者则是默认的端口号1024，两个命令设置的ss密码都是qwerasd）：

![image](https://user-images.githubusercontent.com/98797623/152299779-c24d8995-4040-4ad8-8f5e-820ba35cdfe6.png)

出现如下界面就说明搭建好了：


![image](https://user-images.githubusercontent.com/98797623/152299917-3a0e7d08-0f65-438d-9f8b-c7b387416b90.png)

注：如果需要改密码或者改端口，只需要重新再执行一次搭建ss脚本代码就可以了，或者是修改/etc/shadowsocks.json这个配置文件，之后重启ss服务。

3.相关ss操作

```
修改配置文件：vim /etc/shadowsocks.json
停止ss服务：ssserver -c /etc/shadowsocks.json -d stop
启动ss服务：ssserver -c /etc/shadowsocks.json -d start
重启ss服务：ssserver -c /etc/shadowsocks.json -d restart
```

4.卸载ss服务

```
ss-fly/ss-fly.sh -uninstal
```

## 一键搭建shadowsocksR

再次提醒，如果安装了SS，就不需要再安装SSR了，如果要改装SSR，请按照上一部分内容的教程先卸载SS！！！

1.下载一键搭建ssr脚本（只需要执行一次，卸载ssr后也不需要重新执行）

```
git clone -b master https://github.com/flyzy2005/ss-fly
```

2.运行搭建ssr脚本代码

```
ss-fly/ss-fly.sh -ssr
```

![image](https://user-images.githubusercontent.com/98797623/152300053-f4fb965b-3124-40b9-b7ed-a3783bfc8db0.png)

3.输入对应的参数

执行完上述的脚本代码后，会进入到输入参数的界面，包括服务器端口，密码，加密方式，协议，混淆。可以直接输入回车选择默认值，也可以输入相应的值选择对应的选项：

![image](https://user-images.githubusercontent.com/98797623/152300121-37a115de-4342-4be7-8fbe-aa4aabf84222.png)

全部选择结束后，会看到如下界面，就说明搭建ssr成功了：

```
Congratulations, ShadowsocksR server install completed!
Your Server IP        :你的服务器ip
Your Server Port      :你的端口
Your Password         :你的密码
Your Protocol         :你的协议
Your obfs             :你的混淆
Your Encryption Method:your_encryption_method
 
Welcome to visit:https://shadowsocks.be/9.html
Enjoy it!
```

4.相关操作ssr命令

启动：/etc/init.d/shadowsocks start
停止：/etc/init.d/shadowsocks stop
重启：/etc/init.d/shadowsocks restart
状态：/etc/init.d/shadowsocks status
 
配置文件路径：/etc/shadowsocks.json
日志文件路径：/var/log/shadowsocks.log
代码安装目录：/usr/local/shadowsocks

5.卸载ssr服务

```
./shadowsocksR.sh uninstall
```

# 一键开启BBR加速

[BBR](https://github.com/google/bbr)是Google开源的一套内核加速算法，可以让你搭建的shadowsocks/shadowsocksR速度上一个台阶，本一键搭建ss/ssr脚本支持一键升级最新版本的内核并开启BBR加速。

BBR支持4.9以上的，如果低于这个版本则会自动下载最新内容版本的内核后开启BBR加速并重启，如果高于4.9以上则自动开启BBR加速，执行如下脚本命令即可自动开启BBR加速：

```
ss-fly/ss-fly.sh -bbr
```

![image](https://user-images.githubusercontent.com/98797623/152300367-3e441d52-be7a-4060-919b-7281f61285e3.png)

装完后需要重启系统，输入y即可立即重启，或者之后输入reboot命令重启。

判断BBR加速有没有开启成功。输入以下命令：

```
sysctl net.ipv4.tcp_available_congestion_control
```

如果返回值为：

```
net.ipv4.tcp_available_congestion_control = bbr cubic reno
```

后面有bbr，则说明已经开启成功了。


# 开始使用自己的 VPN

## 各系统的下载地址：

1. Windows客户端下载地址：https://github.com/shadowsocks/shadowsocks-windows/releases?after=2.5.1
2. Mac客户端下载地址：https://github.com/shadowsocks/ShadowsocksX-NG/releases
3. Linux客户端下载地址：https://github.com/shadowsocks/shadowsocks-qt5/wiki/Installation
4. Android/安卓客户端下载地址：https://github.com/shadowsocks/shadowsocks-android/releases。
5. iOS/苹果客户端直接在App Store里搜索SsrconnectPro

## Windows客户端配置

双击运行shadowsocks.exe，之后会在任务栏有一个小飞机图标，右击小飞机图标，选择服务器->编辑服务器：


![image](https://user-images.githubusercontent.com/98797623/152300920-f583c226-89aa-4bc6-ba96-2bf4a16ce1c0.png)

在shadowsocks的windows客户端中，服务器IP指你购买的VPS的IP，服务器端口指你服务器的配置文件中的端口，密码指你服务器的配置文件中的密码，加密指你服务器的配置文件中的加密方式，代理端口默认为1080不需要改动。其他都可以默认。设置好后，点击添加按钮即可。


## MAC OS客户端配置

双击运行shadowsocksX-NG.app，之后会在任务栏有一个小飞机图标，右击小飞机图标，选择服务器->服务器设置：

![image](https://user-images.githubusercontent.com/98797623/152301022-6db654af-d519-4be4-bd79-5221a387219f.png)

在shadowsocks的Mac OS客户端中，地址指你购买的VPS的IP，冒号后面跟上配置文件中的端口，密码指你服务器的配置文件中的密码，加密指你服务器的配置文件中的加密方式。其他都可以默认。设置好后，点击确认即可。

## 安卓客户端配置
下载apk安装好后，打开影梭客户端，点击主界面左上角的编辑按钮（铅笔形状）：

![image](https://user-images.githubusercontent.com/98797623/152301087-f7822053-4397-4232-bbac-a7a026856f28.png)

在shadowsocks安卓客户端的配置中填入相应配置信息，其中，功能设置中，路由改成如上图所示，其他都可以默认。

## 苹果客户端配置
shadowsocks苹果客户端经常会被App Store下架，可以在App Store搜索关键字shadowsock或者wingy，找到一个软件截图中包括填写ip，加密方式，密码的软件一般就是对的了（目前可以用的是FirstWingy）。当然，你也可以下载PP助手，之后在PP助手上下载Wingy（Wingy支持ssr）或者shadowrocket（shadowrocket支持ssr）。

![image](https://user-images.githubusercontent.com/98797623/152301125-c3da2953-9bbf-4a87-9270-82e1f4a2bf4a.png)

# 使用效果


![022翻墙科学上网、免费翻墙、免费科学上网、免费自由上网、fanqiang、翻墙梯子、免费软件/方法，一键翻墙浏览器，shadowsocks/ss/ssr/v2ray/goflyway账号/节点，vps一键搭建翻墙服务器脚本/教程，电脑、手机、iOS、安卓、windows、Mac、Linux、路由器翻墙 一键脚本搭建SS个人VPN搭建翻墙科学上网SSR加速服务并开启BBR教程免费机场 ](https://user-images.githubusercontent.com/98797623/152301311-ab98b364-d0c3-4eac-a97a-f2d66168bf3e.png)






