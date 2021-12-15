# 推流域名配置

目前推流域名配置支持设置推流回调地址和推流鉴权，如需其他配置，请联系技术支持进行非标配置。

在域名管理——推流加速列表，点击需要配置域名后的【详情】，进入域名配置。

![推流域名详情](../ulive/images/2021-域名管理推流加速详情.png)

右边抽屉页面弹出配置详情页，显示基本域名信息和配置信息；

具体域名信息包括，资源ID，接入点，CNAME，业务组，创建时间，状态和推流地址，显示内容均不可修改。

![推流域名配置详情](../ulive/images/2021-推流域名配置详情.png)

配置信息以接入点为粒度显示，可增加或者删除接入点（可批量删除），但最少要有1个接入点，不支持修改接入点名称，支持每个接入点，独立配置推流回调地址和推流鉴权。

![推流域名添加接入点](../ulive/images/2021-推流域名添加接入点.png)

## 推流回调

当主播推流开始或者推流结束时，ULive可以通过客户配置的回调接口，通知客户推流开始或者断开的事件，方便客户对直播流进行管理。

点击设置回调，弹出设置框，可填写用来回调的URL，必须是HTTP/HTTPS开头的URL，点击确定完成配置；配置完成之后，会在接入点页面显示对应配置项。

![推流域名设置回调](../ulive/images/2021-推流域名设置回调.png)

### 示例

推流开始和推流结束的端口需分开配置，示例如下：

1、通知客户推流开始: http://127.0.0.1/publish_start?ip=推流端IP&id=流名&node=节点IP&app=推流域名&appname=发布点

2、通知客户推流结束: http://127.0.0.1/publish_stop?ip=推流端IP&id=流名&node=节点IP&app=推流域名&appname=发布点

其中，publish _ start 和 publish _ stop 为客户提供的回调cgi。

## 设置推流鉴权

直播鉴权功能即为直播“MD5防盗链”。

ULive可以采用对url某些字段进行md5加密的方法，来校验url是否合法，防止域名被盗用，产生高额流量。

客户若有特殊鉴权需求时，请联系UCloud技术支持协助非标配置。

### 鉴权策略

鉴权总体策略为用户按照规则生成如下的链接:

rtmp://abc.com/application/mystream?k=xxxxxx&t=yyyy

1)t为16进制的服务器时间戳

2)k为经过md5加密的字符串，生成规则为:k=md5(约定密钥+流路径+t),

本例中，流路径为"/application/mystream "

ULive服务器会对url进行校验，并检查时间t是否过期。

点击设置鉴权，开启鉴权开关，可设置鉴权Key,和鉴权过期时间，默认过期时间为2小时（120分钟）。

![推流域名设置鉴权](../ulive/images/2021-推流域名设置鉴权.png)

### 示例

假设：

1. 未加密前url为rtmp://vlive3.rtmp.cdn.ucloud.com.cn/ucloud/mytest

2. 当前时间戳为t = 52946dd7

3. 约定密钥为secretkey

则:k=md5(“secretkey”+“/ucloud/mytest”+“52946dd7”) = 2f94cdaf8ea4bdca793e64aba7cb1dea

最终生成的链接如下:

rtmp://vlive3.rtmp.cdn.ucloud.com.cn/ucloud/mytest?t=52946dd7&k=2f94 cdaf8ea4bdca793e64aba7cb1dea
