# FAQ

## Q:为什么视频直播收看时会有卡顿现象？

**A:**
在排除视频直播源本身问题的情况下，视频卡顿有可能是因为播放视频的终端配置过低、局部网络条件欠佳（包括带宽和时延）或播放软件引起的，可以通过改变播放视频的硬件设备、网络环境和软件配置来尝试分析。

## Q:我可以查看哪些统计数据？

**A:** 当前可以查看针对全部直播加速域名的带宽数据及直播性能数据。

## Q:能否提供日志下载功能？

**A:** 提供，可在直播控制台中下载。



## 3. 后台

## Q：如何创建直播加速？

**A:** 请参考`https://docs.ucloud.cn/ulive/guide`

## Q：推流加速与拉流加速有什么区别？

**A:** 推流加速是指客户直接用手机或者pc摄像头，将直播数据推送到ULive的推流节点，客户不需要搭建任何流媒体服务器。

拉流加速是指客户自己搭建流媒体服务器，ulive从该流媒体服务器将直播流拉取并加速。

## Q：现在可以支持哪些直播协议？

**A:** 推流支持rtmp协议；播放支持输出http-FLV/RTMP/HLS；

## Q：可以支持URL防盗链功能么？

**A:**
Ulive采用对url某些字段进行md5加密的方法，来校验url是否合法。客户有鉴权需求时，请联系UCloud技术支持协助配置，并协商好约定的密钥。鉴权总体策略为，用户按照规则生成如下的链接：
`rtmp://abc.com/application/mystream?k=xxxxxx&t=yyyy`

（1）t为16进制的服务器时间戳

（2）k为经过md5加密的字符串，生成规则为：k=md5(约定密钥+流路径+t),

本例中，流路径为"/application/mystream "

Ulive服务器会对url进行校验，并检查时间t是否过期。其中过期时间可以按需求进行配置，默认配置为5分钟。 
示例：
<pre class="pre codeblock"><code>
（1）未加密前url为
 rtmp://vlive3.rtmp.cdn.ucloud.com.cn/ucloud/mytest

（2）当前时间戳为52946dd7

（3）约定密钥为secretkey 则：k = md5(“secretkey”+“/ucloud/mytest”+“52946dd7”) =
2f94cdaf8ea4bdca793e64aba7cb1dea 

最终生成的链接如下： 
rtmp://vlive3.rtmp.cdn.ucloud.com.cn/ucloud/mytest?t=52946dd7&k=2f94cdaf8ea4bdca793e64aba7cb1dea
</code></pre>

## Q：可以对直播进行录制么？

**A:** 支持（内测中），ULive可对将直播录制成mp4或者hls两种格式。具体如下，需要该功能请提交工单。

1、录制条件

1)、直播必须是通过rtmp协议，推流到Ulive。

2)、视频格式必须是h264，音频格式必须是aac。

3)、必须先创建ufile的bucket，用于存储录制的视频。

2、录制视频格式

ULive将直播统一录制为hls。hls具有播放加载时间短，终端播放适配比较好等优点。一般推流结束后4-5秒内，可完成视频的录制。

3、如何开启录制

正常推流默认不进行录制；使用如下参数开启和控制录制：

1)、record=true（必须），设置该路流需要开启录制。

2)、filename=xxx（非必须），设置该路流录制后的文件名为xxx.m3u8，如果没有该参数，则默认使用推流id作为文件名。

下面的推流url表示开启录制，并且指定录制的文件名为myfile.m3u8：'rtmp://publish3.cdn.ucloud.com.cn/ucloud/stream?record=true&filename=myfile'

4、视频智能拼接

主播在直播过程中，如果推流有断开并重推，只要断开时间在10分钟以内，则重推的视频将与之前的视频合并，生成一个录制文件（适用于多次重推）；如果断开10分钟以后再重推，则重推会被视为另外一次推流，生成的录制文件将会覆盖之前的文件。该功能主要用于解决主播推流被临时中断的情况，比如网络抖动或者接听电话导致的推流断开情况。

5、如何播放录制的文件

申请ufile的bucket后，ufile会生成默认的加速域名，已经录制好的文件，可以通过加速域名来访问，访问地址为：'http://加速域名/m3u8文件名';
 
假设您申请的bucket名称为mybucket，录制的文件名为myfile，那么录制文件的播放地址为：'http://mybucket.ufile.ucloud.com.cn/myfile.m3u8' 


6、录制回调功能

文件录制完成后，可以回调客户的接口，通知录制的文件名、文件大小、时长等信息。回调的url格式如下：

<pre class="pre codeblock"><code>  
http:%%//%%接口地址?filename=文件名&filesize=文件大小&spacename=bucket名称&duration=视频时长
以下是一个回调的例子：
http://cgi.ucloud.com.cn/record_callback?filename=300000039_1462860643.m3u8&filesize=13719488&spacename=record&duration=163
</code></pre>

7、如何测试直播录制

Ulive提供录制的测试环境，方便客户进行测试联调。测试环境的推流域名为：publish3.cdn.ucloud.com.cn，接入点为：ucloud，录制的文件存储在ulive-record这个bucket中。

假设您的直播流id是mystream，想要录制的文件名是myfile.m3u8，则使用此的推流地址即可进行录制:'rtmp://publish3.cdn.ucloud.com.cn/ucloud/mystream?record=true&filename=myfile'

当您推流结束后，您可以通过如下地址播放录制好的视频：'http://ulive-record.ufile.ucloud.com.cn/myfile.m3u8'
 
## Q：我能对直播过程截图么？

**A:** 支持，ULive支持周期性截取视频关键帧，并保存到对象存储。需要该功能请提交工单。

## Q：直播视频的延迟大约有多少？

**A:**
直播视频的延迟从端到端角度考虑会涉及输入或输出设备，以及中间采用的协议。下行HLS协议的方式延迟会显著高于RTMP协议。在不同网络状况下，会有差异。通常HLS协议的最低延迟在5-7s左右（需要原始流关键帧间隔为1s左右）；RTMP/FLV协议的延迟在3s左右，如果需要更端的延时，可在播放器端减小缓存来实现。

## Q：如何优化直播延迟？

**A:** 在网络确定的情况下，直播延迟与推流的关键帧间隔相关，一般关键帧间隔越短，则直播延迟越低，推荐的关键帧间隔为1-2秒。

## Q：推流码率是否有限制？

**A:**视频直播服务不限制推流码率，支持常见分辨率以及对应码率；为避免推流卡顿，建议码率不超过4Mbps。

## Q：如何对直播节目进行禁播和解禁？

**A:**当主播直播不健康的节目时，可以调用我们的禁播api，立即将直播节目禁止推流和播放(需联系技术支持配置)。示例如下：

加入域名为publish.ucloud.com.cn，接入点为live，流ID为123。

那么可如下调用该接口禁播：
`https://api.ucloud.cn/?Action=ForbidLiveStream\&Domain=publish.ucloud.com.cn\&Application=live\&StreamId=123`

可调用如下接口解禁：
'https://api.ucloud.cn/?Action=UnforbidLiveStream&Domain=publish.ucloud.com.cn&Application=live&StreamId=123' 
 
## Q：如何获取推流状态？

**A:**
ULive通过回调客户接口，通知当前推流状态。当主播推流开始或者推流结束时，ULive可以通过客户配置的回调接口，通知客户推流开始或者断开的事件，方便客户对直播流进行
管理。客户需要回调功能时，请联系技术支持进行配置。推流开始和推流结束的端口需分开配置，示例如下：
<pre class="pre codeblock"><code> 
 
1、通知客户推流开始：

<http://127.0.0.1/publish_start?ip=推流端IP&id=流名&node=节点IP&app=推流域名&appname=发布点>

2、通知客户推流结束：

<http://127.0.0.1/publish_stop?ip=推流端IP&id=流名&node=节点IP&app=推流域名&appname=发布点>
其中，publish\_start和publish\_stop为客户提供的回调cgi。
 </code></pre>

## Q：可以在直播中支持广告么？

**A:** 暂不支持。该功能将在未来版本中发布。

## Q：可以在直播中支持弹幕交互么？

**A:** 暂不支持。该功能将在未来版本中发布。

## Q：如果要更换推流域名，需要修改些什么？

**A:** 以修改demo的推流地址为例，需

1、搜索”publish3.cdn.ucloud.com.cn”找到对应代码，修改地址为新的推流地址；

2、联系客户经理或技术支持；

3、添加新的推流域名授权，ucloud为您提供与新推流域名配对的推流key；

4、更换demo中的key”publish3-key”为新的推流key

## Q：推流SDK支持推荐使用哪种编码模式？

**A:** iOS：目前只有硬编码模式，客户无需选择；

Android：支持硬编码和软编码两种模式。硬件编码支持滤镜功能，编码效率较高，API18或以上可以使用。目前软编码暂时不支持滤镜功能，但兼容性较好，API要求较低，API9或以上即可。

## Q. 是否支持海外直播

**A:** 暂时不支持海外直播。

