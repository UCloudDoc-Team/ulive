# 视频预处理

{{indexmenu_n>4}}

视频预处理是指视频上传后，可以根据预定义的一些规则，自动对视频进行处理，无需额外的人工操作。

视频预处理由对象存储（UFile）与媒体工厂（UMedia）共同完成，其实现方式是通过对象存储的上传策略，指定媒体工厂的处理接口和参数，达到自动处理的目的。

## 操作指南

客户如果需要使用视频预处理功能，自动创建视频处理任务，则可以在确认好视频处理模版以及其他参数后，联系UCloud技术支持同事协助创建预处理策略。

预处理策略创建完成后，用户可以通过[UFile上传策略](https://docs.ucloud.cn/storage_cdn/ufile/putpolicy)回调UMedia的预处理接口，传入预处理策略的名称以及当前文件名，来实现预处理功能。

UMedia预处理接口地址为：<http:%%//%%inner.umedia.ucloud.com.cn/CreateUmediaTask>

## 用例参考

### 第一步：创建视频处理模版

通过控制台或调用API创建。假设现有两个视频处理模版，模版ID分别为0和1。

### 第二步：联系后台配置预处理策略

将模版ID（0和1）告知UCloud技术支持同事，由UCloud后台针对该模版配置预处理策略，生成预处理规则。假设生成的规则名为mypolicy。

### 第三步：指定UFile上传策略

用户在上传UFile时，指定如下的回调参数：

    {
     "callbackUrl" : " http://inner.umedia.ucloud.com.cn/CreateUmediaTask",
     "callbackBody" : "url=http://demo.ufile.ucloud.cn/test.mp4& patten_name=mypolicy" // url为文件上传后的地址
    }

上传成功并且创建完视频处理任务,UFile服务将返回:

    {
     "Action" : "CreateUmediaTaskResponse",
     "RetCode" : 0,
     "Message" : "succeed"
    }
