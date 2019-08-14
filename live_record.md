# 扩展功能

{{indexmenu_n>4}}

## 直播转码

直播转码是指在直播的过程中，通过UCloud转码系统，将直播流进行转码处理。用户可通过转码规则指定的后缀播放转码后的直播流。

**直播转码功能配置请参考操作指南**

### 如何使用转码

转码为被动功能，当用户通过转码规则中全局唯一的转码后缀播放转码视频时，触发转码功能开启。当直播流结束后转码结束。

**示例**

 接入点：test

 rtmp播放域名：rtmp.company.com

 hls播放域名：hls.company.com
 
 rtmp播放地址：
 rtmp:%%//%%rtmp.company.com/test/{streamid}>
 
 hls播放地址：
 http:%%//%%hls.company.com/test/{streamid}/playlist.m3u8

若配置了转码规则(转码后缀：500k)且需要播放转码后的视频，则播放地址为：

rtmp播放地址  rtmp:%%//%%rtmp.company.com/test/{streamid}_500k

hls播放地址  http:%%//%%hls.company.com/test/{streamid}_500k/playlist.m3u8

## 直播录制

视频直播录制是指在直播的过程中，录制系统将直播的数据存储下来，并进行处理，上传到ufile对象存储的过程。

**直播录制功能配置请参考操作指南**

### 录制条件

1)、直播必须是通过rtmp协议，推流到ULive。

2)、视频格式必须是h264，音频格式必须是aac。

3)、必须先创建ufile的bucket，用于存储录制的视频。

### 如何开启录制

如果配置的录制规则为“强制录制”，则保证录制规则为“开启”状态后推流即可录制。

如果配置的录制规则为“选择性录制”，则正常推流默认不进行录制；使用如下参数开启和控制录制：

1)、record=true（必须），设置该路流需要开启录制。

2)、filename=xxx（非必须），设置该路流录制后的文件名为xxx.m3u8，如果没有该参数，则默认使用推流id作为文件名。**(仅支持hls录制)**

下面的推流url表示开启录制，并且指定录制的文件名为myfile.m3u8：
rtmp:%%//%%publish3.cdn.ucloud.com.cn/ucloud/stream?record=true&filename=myfile


### 录制文件默认命名规则

flv录制：域名+流名+日期\_时间.flv

mp4录制：域名+流名+日期\_时间.mp4

hls录制：域名+流名+文件名.m3u8 其中文件名由用户推流时指定**(仅支持hls录制)**，如果没有指定，则为：域名+流名+流名.m3u8


### 视频智能拼接(仅支持hls录制)

主播在直播过程中，如果推流有断开并重推，只要断开时间在10分钟以内，则重推的视频将与之前的视频合并，生成一个录制文件（适用于多次重推）；

如果断开10分钟以后再重推，则重推会被视为另外一次推流，生成的录制文件将会覆盖之前的文件。

该功能主要用于解决主播推流被临时中断的情况，比如网络抖动或者接听电话导致的推流断开情况。


### 录制回调功能

#### flv/mp4录制回调

文件录制完成后，可以回调客户的接口(需在配置录制规则时填写)，通知录制的文件名、文件大小、时长等信息。回调的url格式如下：(POST请求)

http:%%//%%接口地址?filename=文件名&filesize=文件大小&spacename=bucket名称&duration=视频时长&url=视屏url地址

以下是一个回调的例子：

http:%%//%%cgi.ucloud.com.cn/record_callback?publishdomain=publish-test.ucloud.com.cn&streamid
=test&filesize=5236598745&duration=22&url=http:%%//%%wangqiguoy.cn-bj.ufileos.com/test.flv

视频时长单位：秒，文件大小单位：字节。

#### hls录制回调

hls录制回调的url格式如下：(POST请求)

http:%%//%%接口地址?filename=文件名&filesize=文件大小&spacename=bucket名称&duration=视频时长

以下是一个回调的例子：

http:%%//%%cgi.ucloud.com.cn/record_callback?filename=test.m3u8&filesize=343&spacename=bucket_test&duration=50

视频时长单位：秒，文件大小单位：字节。

### 如何测试直播录制

Ulive提供录制的测试环境，方便客户进行测试联调。测试环境的推流域名为：publish3.cdn.ucloud.com.cn，接入点为：ucloud，录制的文件存储在ulive-record这个bucket中。

假设您的直播流id是mystream，想要录制的文件名是myfile.m3u8，则使用如下的推流地址即可进行录制：

rtmp:%%//%%publish3.cdn.ucloud.com.cn/ucloud/mystream?record=true&filename=myfile

当您推流结束后，您可以通过如下地址播放录制好的视频：http:%%//%%ulive-record.ufile.ucloud.com.cn/myfile.m3u8

## 纯音频/视频输出

纯音频/视频输出通过在播放地址指定相应参数实现。支持rtmp/http-flv/hls三种协议。

在播放地址后添加?only-audio=1参数，表示输出纯音频流

在播放地址后添加?only-video=1参数，表示输出纯视频流

**例如：**

需要在rtmp播放域名：vlive3.rtmp.cdn.ucloud.com.cn下播放纯音频流，则指定下面的URL进行播放：

rtmp:%%//%%vlive3.rtmp.cdn.ucloud.com.cn/ucloud/test?only-audio=1

## 直播流封禁/解禁

当线上直播内容存在涉黄或者其他不健康内容时，可以调用ULive标准API，对直播流进行秒级禁播。

对一个流ID调用禁播接口后，正在直播的内容会断流，观众无法播放，主播重试推流也会失败，直到调用解禁接口对该流ID进行解禁。

API接口及使用方式请参考[直播流封禁/解禁文档](http://product-tools.cn-bj.ufileos.com/ULive/Ulive直播禁播&解禁文档.pdf)。

## 直播推流状态回调

当主播推流开始或者推流结束时，ULive可以通过客户配置的回调接口，通知客户推流开始或者断开的事件，方便客户对直播流进行管理。

**客户需要回调功能时，请联系技术支持进行配置。**

#### 示例

推流开始和推流结束的端口需分开配置，示例如下：

1、通知客户推流开始:
http:%%//%%127.0.0.1/publish_start?ip=推流端IP&id=流名&node=节点IP&app=推流域名&appname=发布点

2、通知客户推流结束:
http:%%//%%127.0.0.1/publish_stop?ip=推流端IP&id=流名&node=节点IP&app=推流域名&appname=发布点

其中，publish _ start 和 publish _ stop 为客户提供的回调cgi。

## 直播鉴权

直播鉴权功能即为直播“防盗链”。

ULive可以采用对url某些字段进行md5加密的方法，来校验url是否合法。防止域名被盗用，产生高额流量。

**客户有鉴权需求时，请联系UCloud技术支持协助配置，并协商好约定的密钥。**

### 鉴权策略

鉴权总体策略为用户按照规则生成如下的链接:

rtmp:%%//%%abc.com/application/mystream?k=xxxxxx&t=yyyy

1)t为16进制的服务器时间戳

2)k为经过md5加密的字符串，生成规则为:k=md5(约定密钥+流路径+t),

本例中，流路径为"/application/mystream "

ULive服务器会对url进行校验，并检查时间t是否过期。其中过期时间可以按需求进行配置，默认配置为5分钟。

### 示例

假设：

1) 未加密前url为rtmp:%%//%%vlive3.rtmp.cdn.ucloud.com.cn/ucloud/mytest

2) 当前时间戳为t = 52946dd7

3) 约定密钥为secretkey

则:k=md5(“secretkey”+“/ucloud/mytest”+“52946dd7”) =
2f94cdaf8ea4bdca793e64aba7cb1dea

最终生成的链接如下:

rtmp:%%//%%vlive3.rtmp.cdn.ucloud.com.cn/ucloud/mytest?t=52946dd7&k=2f94
cdaf8ea4bdca793e64aba7cb1dea