# 直播流管理

直播流管理提供推流域名流查询，包括在线流，历史流以及禁推流三种。

## 在线流

通过域名查询，也可以通过域名+流名称查询，展示对应域名的流名称、接入点、推流端IP、开始推流时间和在线人数数据，并支持对在线流禁推。

![在线流](../images/2021-直播流管理在线流.png)

点击【流监控】，可查看单个流信息

![在线流监控](../images/2021-直播流管理在线流监控数据.png)

可以调用ULive标准API，获取[在线推流记录列表](https://docs.ucloud.cn/api/ulive-api/get_u_live_dom_real_stream_list_info)。

## 历史流

通过域名查询时间段内的推流信息，也可以通过域名+流名称查询，展示对应流名称、接入点和时间段，点击【流监控】，可查看单个流信息。

![历史流](../images/2021-直播流管理历史流.png)

可以调用ULive标准API，获取[历史推流记录列表](https://docs.ucloud.cn/api/ulive-api/get_u_live_history_stream_list)。

## 禁推流

查看推流域名已经设置禁推的流记录，也可以解除禁推。

![禁推流](../images/2021-直播流管理禁推流.png)

当线上直播内容存在涉黄或者其他不健康内容时，可以调用ULive标准API，对直播流进行秒级禁播。

对一个流ID调用禁播接口后，正在直播的内容会断流，观众无法播放，主播重试推流也会失败，直到调用解禁接口对该流ID进行解禁。

API接口及使用方式请参考[直播流封禁](https://docs.ucloud.cn/api/ulive-api/forbid_live_stream)/[直播流解禁](https://docs.ucloud.cn/api/ulive-api/unforbid_live_stream)文档。
