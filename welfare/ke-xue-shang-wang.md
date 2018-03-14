# 科学上网

一直有一个亚马逊的羊毛，不知道大家撸没撸过，没撸过就来看看吧，可以免费科学上网一年。

使用的是shadowsocket实现

#### 第一步，注册

1. 撸亚马逊的羊毛，首先当然是注册亚马逊账号了，搜索AWS（Amazon Web Services），进入网址 [https://amazonaws-china.com/cn/free/](https://amazonaws-china.com/cn/free/)
2. 注册亚马逊账号，填写个人信息，需绑定一张信用卡
3. 免费云服务也是有限制的，每月750小时（24\*31😆），每月100w次请求...
4. 接下来会有一个验证码，会打电话过来，输入屏幕上的四个数字，之后输入 \* ，就可以成功激活了

#### 第二步，创建实例

1. 登录aws主页，点击右上角我的账户
2. 右上角用户名边上有一个地区选择，根据自己的需求选择一个位置创建主机，如果只是上网用，建议东京
3. 点击启动实例，选择一个Linux系统，推荐使用Ubuntu Server 16.04 LTS\(HVM\)，记得选择的时候选带有符合条件的免费套餐
4. 之后点击启动，会让你创建密钥，输入一个名字，之后下载存储秘钥
5. 启动实例，就可以再你的服务器中看到了，服务器名，dns，ip等，记录下来ip

#### 第三步，连接实例

1. 点击启动实例后面的连接，里面会有多种连接方式，推荐大家使用ssh连接
2. 使用ssh连接需要使用先前生成的秘钥
3. 窗口出现ubuntu@x-x-x表示成功

#### 第四步，安装软件

1. 提升权限，安装软件
2. sudo -s，进入root用户
3. apt update，更新软件源
4. apt install python-pip，安装python包管理工具
5. pip install shadowsocks，安装科学上网软件
6. 安装锐速(锐速不支持Openvz！)TCP加速
    - `` wget -N --no-check-certificate https://github.com/91yun/serverspeeder/raw/master/serverspeeder.sh && bash serverspeeder.sh`` 

#### 第五步，配置软件

1. 编写一个配置文件，在/etc/shadowsocks.json中编写配置（如果没有就创建）

2. ```
   单用户配置:
       {
           "server":"0.0.0.0",
           "server_port":"9229",
           "local_address":"127.0.0.1",
           "local_port":"1080",
           "password":"自己的密码",
           "timeout":500,
           "method":"aes-256-cfb",
           "fast_open":false
       }

   多用户配置:
       {
           "server":"0.0.0.0",
           "server_port":"9229",
           "local_address":"127.0.0.1",
           "local_port":"1080",
           "port_password":{
               "9229":"密码",
               "9230":"密码",
               "9231":"密码"
           }
           "timeout":500,
           "method":"aes-256-cfb",
           "fast_open":false
       }
   ```

   1. 建议其实单个用户的配置足够，一个账户也可以多个设备登录

#### 第六步，启动服务器

1. 在终端中启动服务器ssserver -c /etc/shadowsocks.json -d start   
2. 加入开机自启，编辑/etc/rc.local ，将启动指令粘贴到此
3. 去服务器配置中打开端口，到自己的实例上，到最右边找到安全组，进入安全组设置，点击左下角的入站，编辑，点击添加规则，在端口范围里填上我们设置的端口，来源下拉框中选择任何位置。

#### 第七步，连接使用

1. 在Android手机上可以使用影梭进行连接
2. 在mac，linux，windows上可以使用shadowsocks客户端，都是开源的

3. windows版本[https://github.com/shadowsocks/shadowsocks-windows](https://github.com/shadowsocks/shadowsocks-windows)

4. linux，mac版本[https://github.com/shadowsocks/shadowsocks-qt5](https://github.com/shadowsocks/shadowsocks-qt5)
5. android版本[https://github.com/shadowsocks/shadowsocks-android](https://github.com/shadowsocks/shadowsocks-android)



#### 你可能需要：
* 如果你不知道你的机子到底是不是Openvz，请食用[《教程：一键检测VPS是Openvz还是KVM还是Xen》](http://www.91yun.org/archives/836)
* 如果你的内核不对，是Centos的话请食用[《教程：CentOS更换内核，提供锐速可用的内核下载》](http://www.91yun.org/archives/795)。debian和ubuntu我不熟，暂时还没一键包，请自行百度google。。
