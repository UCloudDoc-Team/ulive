{{indexmenu_n>13}}

# WEB SDK指南

## 1\. 下载资源

  - 可以下载Demo、SDK、API文档  
    [现在下载](https://github.com/ucloud/urtc-js-demo.git)

## 2\. 集成SDK

  - 可使用script直接引入  
    \* 建议使用chrome60以上版本



``` javascript
 <script src="urtcsdk-1.0.1.js"></script>
```

## 3\. 初始化

``` javascript
var UCloudRtcEngine = new UCloudRtcEngine();
UCloudRtcEngine.init({
        app_id: appData.appId,//项目的appid
        room_id: appData.roomId,//进入的房间id
        user_id: appData.userId,//用户的id
    }).then(function(data){
    //返回当前用户的token
    },function(err){
})
```

## 4\. 建立通话

  - 登陆房间  
    `UCloudRtcEngine.joinRoom({
                                                    token: getToken//初始化时获得的token
                                    }).then(function(e){
                                                    //加入房间成功
                                    },function(err){
                                                    //加入房间失败
                                    })
    `
  - 获取本地音视频流  
    `UCloudRtcEngine.getLocalStream({
                                                    media_data:’videoProfile640*360’,//推流相关配置的属性（分辨率宽度*分辨率高度）
                                                    video_enable:true,//是否采集视频
                                                    audio_enable:true,//是否采集音频
                                                    media_type:1 //MediaType 1 cam 2 desktop
                                    }).then(function(data){
                                                //音视频流数据
                                    },function(e){
                                                    //错误信息
                                    })
    
    `



  - 发布本地流  



``` javascript
UCloudRtcEngine.leaveRoom({
            user_id:user_id,//用户id
            media_type:1,//发布的流类型 1 摄像头 2桌面
    audio: true,//是否包含音频流
    video:true,//是否包含视频流
    data:false//是否包含数据流
        }).then(function(e){
            //发布成功
        },function(err){
             //发布失败
        });

```

  - 订阅远端流  



``` javascript
UCloudRtcEngine.subscribe({
            media_type: 1,//订阅的流类型 1 摄像头 2桌面
    stream_id: “stream_id”,//订阅流id
    user_id: “user_id",//订阅用户id
        },{
    audio_enable: true,//是否包含音频流
    video_enable: true//是否包含数据流
}).then(function(e){
            //发布成功
        },function(err){
             //发布失败
        });

```

    *获取本地音量数据

``` javascript
UCloudRtcEngine.getAudioVolum().then(function(data){
               //音量数据
         },function(err){
    //错误信息
})

```

  - 关闭/打开本地音视频



``` javascript
UCloudRtcEngine.activeMute({
            stream_id: stream_id,//媒流id
            stream_type: 1,//1 发布流 2 订阅流
            user_id:user_id,//用户id
            track_type: 2,//1 视频 2音频
            mute: video_enable//true 禁用 false 开启
        }).then(function(e){
    //操作成功
    },function(err){
    //错误信息
});

```

  - 枚举本地媒体设备  



``` javascript
UCloudRtcEngine.getLocalDevices().then(function(e){
    //成功输出本地设备数据
     //microphones 音频输入设备列表 
    //speakers 音频输出设备列表
    //cameras 视频输输入设备列表
    //设备列表中的每一个元素类型相同（label：设备名称，deviceId：设备Id） 
},function(err){
    //失败
})

```

  - 离开房间  



``` javascript
UCloudRtcEngine.leaveRoom({
            room_id: room_id//房间id
        }).then(function(e){
            //退出成功
        },function(err){
             //退出失败
        });

```
