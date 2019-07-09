# 开发指南

{{indexmenu_n>7}}

客户端管理工具支持的功能包括：

1.  文件分片上传
2.  删除文件



  -  \* 

## 使用说明

uvideomgr-win64.exe \~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~

从UCloud官网上找到对应的公钥和私钥填写在config.cfg配置文件中

``` python
./uvideomgr-win64.exe --action mput --bucket bucketname --dir localdir
./uvideomgr-win64.exe --action mput --bucket bucketname --key key --file localfile
./uvideomgr-win64.exe --action delete --bucket bucketname --key key
```

### 文件分片上传

上传目录

``` python
./uvideomgr-win64.exe --action mput --bucket jiahui --dir D:\FFOutput    
成功提示如：
2015/12/09 15:02:44.650585 [INFO]Upload File[ jiahui : D:/FFOutput/Wildlife.mp4 ] Success
2015/12/09 15:02:48.409288 [INFO]Upload File[ jiahui : D:/FFOutput/Wildlife.wmv ] Success
```

上传单个文件

``` python
./uvideomgr-win64.exe --action mput --bucket jiahui --key Wildlife.wmv --file ./Wildlife
```

### 删除文件

``` python
./uvideomgr-win64.exe --action delete --bucket jiahui --key Wildlife.wmv
成功提示如：
2015/12/09 16:58:31.833056 [INFO]Delete [jiahui:Wildlife.wmv] success
```

#### uvideomgr-linux64

从UCloud官网上找到对应的公钥和私钥填写在config.conf配置文件中

``` python
./uvideomgr-linux64 mput spacename remotefilename localfilename
./uvideomgr-linux64 delete spacename remotefilename
```

### 文件分片上传

``` python
./uvideomgr-linux64 mput jiahui Wildlife.mp4 ./Wildlife.mp4
成功提示如：
mput file success
```

### 删除文件

``` python
./uvideomgr-linux64 delete jiahui Wildlife.mp4 
成功提示如：
delete file success
```
