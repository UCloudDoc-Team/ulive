# 实时监控
Ulive云直播平台提供实时监控功能，实时监控服务包括以下功能

|   监控项   |   说明    |
|-----------|----------|
|剩余流量/日带宽峰值|若您选择的计费方式为预付费流量包，则显示剩余流量，剩余流量=所购流量包总流量-已使用流量。</b>若您选择的计费方式为预付费流量包，则显示为日带宽峰值。|
|当前计费模式|可选择预付费流量包或者日峰值后付费进行计费（二选一），若选择日峰值后付费，则已购买的流量包不会再使用；若需要使用月付费，请与客户经理联系，修改为月付时，当前计费模式显示为：按月后付费。|
| 带宽/流量  |展示用户在当前时间粒度内直播播放产生的下行带宽，计费按照下行带宽进行收费。</b>系统默认展示最近一天的监控情况，也可根据需求选择查询时间粒度，最长支持查询32天的数据；</b>若使用高级筛选，可根据分运营商或者分地区进行查看，最长支持查询30天的数据。|
|  状态码   |查看域名状态码情况，支持1XX\2XX\3XX\4XX\5XX状态码。|
|推流并发数|展示推流域名的在线流数。|
|观众在线数|展示播放域名的在线观看人数。|
|直播流ID监控|查询单个域名根据流ID对应的推流帧率，推流码率，播放带宽和观看人数。|

## 剩余流量/日带宽峰值

通过当前计费模式，可调整计费方式，若已购买流量包，当切换为日峰值计费之后，无法使用已购买的流量；</b>已购买流量包无使用时限，已购买的流量包30个自然日内未使用，可联系客户经理退费到余额，若已经使用流量包、或者购买流量包超过30个自然日（不管是否使用），均不支持退费。

![计费模式选择](/ulive/image/2021-计费模式选择.png)

![预付费流量包](/ulive/image/2021-预付费流量包.png)

![日带宽峰值计费](/ulive/image/2021-日带宽峰值后付费.png)

## 带宽/流量

通过带宽、流量可查看当前服务量级情况，显示用户在当前时间粒度内的播放带宽/流量（下行）。

默认显示最近1天的数据，时间粒度为5分钟，可调整为按1分钟粒度，小时以及天粒度进行查看；当查看时间范围超过7天，则无法查看1分钟粒度的数据。

查看时间范围最长不超过32天。

通过高级筛选，可查看分运营商分地区数据。

![实时监控带宽](/ulive/image/2021-实时监控带宽.png)

![实时监控流量](/ulive/image/2021-实时监控流量.png)


## 状态码

查看域名状态码情况，支持1XX、2XX、3XX、4XX和5XX状态码查，通过勾选状态码可分别查看对应状态码信息。

![实时监控状态码](/ulive/image/2021-实时监控状态码.png)

## 推流并发数

展示推流域名的在线流数，域名选择只能选推流域名，可查询单个或者多个域名的数据。

![实时监控推流并发数](/ulive/image/2021-实时监控推流并发数.png)

## 观众在现数

展示播放域名的在线观看人数，可查询单个或者多个域名的数据。

![实时监控观众在线数](/ulive/image/2021-实时监控观众在线数.png)

## 直播流ID监控

查询单个域名根据流ID对应的推流帧率，推流码率，播放带宽和观看人数。

![实时监控直播流ID监控](/ulive/image/2021-实时监控直播流ID监控.png)










