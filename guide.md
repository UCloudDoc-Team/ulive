\==========快速上手===========

{{indexmenu_n>2}}

本章目的在于指导初次使用的用户如何快速上手使用直播云。

## 创建直播加速

### Step1. 选择计费模式

进入ULive产品界面，点击【选择计费模式】。

![](/images/ulive选择计费方式.jpg)

计费模式分为两种：流量计费和带宽计费，请选择适合您业务的计费模式。计费规则请参考：[产品价格](https://docs.ucloud.cn/video/ulive/charge)

注：若要开通带宽计费，需提前联系客户经理开通后付费权限。

### Step2. 创建推/拉流加速

此处以创建推流加速为例。

进入\[域名管理\]页面，点击\[创建推流加速\]按钮。

若您选择流量计费，则需先购买流量包才能创建域名。
若您选择带宽计费，需保证账户余额>0才能创建域名。

![](/images/创建推流加速.jpg)

![](/images/创建推流加速页面.jpg)

在弹出的页面中填写信息：

1） 推流域名：请填写用于推送rtmp直播流的域名，请确保域名的唯一性

2） 接入点：请自定义一个rtmp推流点，注意必须为数字、字母或“-”。

3） 播放域名：请填写播放rtmp或者hls协议直播流的域名。后台只会配置已勾选的协议，两个播放协议至少勾选一个。

4） 直播名称：请填写推送和播放直播流的流名称，可任意指定（仅限于英文字母、数字、下划线）。

PS:
1、推流域名与各个协议的播放域名必须两两互不相同。
2、使用的域名需经过工信部备案

> 例如：
> 
> 推流域名：publish.company.com，接入点：test
> 
> rtmp播放域名：rtmp.company.com，hls播放域名：hls.company.com
> 
> 则推流地址为：[rtmp://publish.company.com/test/{streamid}](rtmp://publish.company.com/test/%7Bstreamid%7D)
> 
> rtmp播放地址为：[rtmp://rtmp.company.com/test/{streamid}](rtmp://rtmp.company.com/test/%7Bstreamid%7D)
> 
> hls播放地址为：[http://hls.company.com/test/{streamid}/playlist.m3u8](http://hls.company.com/test/%7Bstreamid%7D/playlist.m3u8)

### Step3. 等待域名配置

当所有信息填写完成，点击确定，提交加速请求，等待UCloud审核。审核将在**工作日**2小时内完成，如果超过2小时还未审核通过，请联系我司技术支持（qq：4000188113，tel：4000188113）或者客户经理进行咨询。审核完成后，还需要到dns配置cname记录，配置cname记录后才能完成加速。

### Step4. dns配置cname记录

添加加速后，推流域名和播放域名都会提供一个cname，需要在自己的DNS服务商处添加此cname，才能完成加速。

1） 到dns服务商处删除a记录，添加cname记录，如下图示例

2） 在我的域名title下，添加要设置的域名，如果已经添加，请点击添加的域名， 然后点击添加记录按钮，如下图：

![](/images/cname1.png)

![](/images/cname2.png)

主机记录，指域名前缀，如：创建的加速域名为static.ucloud.cn，域名为ucloud.cn，前缀为static；
记录类型，请选择cname类型；
线路类型，默认类型是网络类型，一般选默认，如果有特别需要可以换其他运营商;
记录值，即ucloud提供的cname，域名审核通过后，可以在ulive域名管理界面中查询；
mx优先级，设置cname记录不需要设置mx优先级；
ttl， 指资源记录的更新时间，即多久从dns服务器上读取最新记录，默认单位是秒，一般选择默认值；

3） 配置所有参数后，点击保存，dns配置cname记录步骤完成。

cname记录与其他类型的同名记录可能存在冲突，导致所有记录不生效，填写时请注意。
