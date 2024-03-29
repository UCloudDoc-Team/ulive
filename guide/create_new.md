# 创建直播加速域名

### 操作说明

直播加速域名分为推流域名和播放域名，每个账户最多可添加<strong>10</strong>个域名，加速内容必须合法且符合业务规范，若因业务需要增加域名配置上限，请与技术支持联系。

初次创建加速域名时，需选择计费方式并且新增第一个域名，再次新增加速域名，则无需选择计费方式。

直播不支持泛域名加速，当前创建加速默认为<strong>国内加速</strong>，暂不支持海外直播加速。

## 创建推流加速

* 1.推流加速：是指将直播流推到UCloud云直播中心，通过播放加速来分发。

![推流域名管理列表](../../master/images/2021-推流域名管理列表.png)

* 2.点击【创建推流加速】后，请填写如下配置参数，详细见参数说明。

![2021-创建推流域名](../../master/images/2021-创建推流域名.png)

| 配置项   | 说明                                                         |
| -------- | ------------------------------------------------------------ |
| 推流域名 | 推流域名，如example.com，不能以HTTP或者HTTPS开头；<br />当前仅支持国内直播加速，根据国家工信部规定，<strong>域名必须备案</strong>；<br />账户维度默认加速域名配额数量10个。 |
| 接入点   | 直播推流接入点，支持英文字母、数字和符号,支持* ，代表所有接入点。     |
| 业务组   | 在对应的项目下设置不同的业务组进行资源管理。                 |

## 创建播放加速

* 1.播放加速：指直播拉流加速，将直播中心的直播流进行分发

![2021-播放域名管理列表](../../master/images/2021-播放域名管理列表.png)

* 2.点击【创建播放加速】后，请填写如下配置参数，详细见参数说明。

![2021-创建播放加速](../../master/images/2021-创建播放加速.png)

![2021-播放域名自定义源站](../../master/images/2021-播放域名自定义源站.png)

![2021-源站地址生成器](../../master/images/2021-源站地址生成器.png)


| 配置项      | 说明                                                         |
| ----------  | ------------------------------------------------------------ |
| 播放域名    | 播放域名，如example.com，不能以HTTP或者HTTPS开头；<br/>当前仅支持国内直播加速，根据国家工信部规定，<strong>域名必须备案</strong>；<br />账户维度默认加速域名配额数量10个。 |
| 回源配置    | 指进行播放加速时，加速的直播流是从哪里获取；<br/>选择推流域名或者自定义源站；<br />当为推流域名时，请选择您在UCloud创建的推流加速域名，接入点同推流加速接入点；<br />当为自定义源站时，可以是IP或者源站域名或在其他提供直播加速服务厂商的推流域名，同时需要定义接入点、回源协议、回源APP和回源端口；<br />可使用回源地址生成器生成。 |
| 业务组      | 在对应的项目下设置不同的业务组进行资源管理。                 |

#### 推拉流地址示例：

例如：推流域名：publish.company.com，接入点：test，播放域名：play.company.com

推流地址为： rtmp://publish.company.com/test/{streamid}

播放地址为：

* RTMP播放地址： rtmp://play.company.com/test/{streamid}
* FLV播放地址：http://play.company.com/test/{streamid}.flv
* HLS播放地址：http://play.company.com/test/{streamid}/playlist.m3u8
