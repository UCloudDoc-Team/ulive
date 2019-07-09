# Python SDK

{{indexmenu_n>6}}

本源码包含使用Python对UCloud的对象存储业务进行空间和内容管理的API，适用于Python 2和Python 3

## 1\. 依赖的Python Package

**requests**

## 2\. 文件目录说明

  - ucloud文件夹： SDK的具体实现
  - setup.py: package安装文件
  - test文件夹: 测试文件以及demo示例

## 3\. 使用方法

> 将ucloud目录复制到工程项目下

或者

> python setup.py install

## 4\. 功能说明

### 公共参数说明

``` python
public_key = ''      #账户公私钥中的公钥

private_key = ''    #账户公私钥中的私钥

# 设置参数
from ucloud.uvideo import config

    #设置云视频上传host,外网可用 uploadvideo.ucloud.cn
    config.set_default(uploadsuffix='YOUR_UPLOAD_SUFFIX')
    #设置下载host后缀，比如CDN下载 .uvideo.ucloud.com.cn
    config.set_default(downloadsuffix='YOUR_DOWNLOAD_SUFFIX')
    #设置请求连接超时时间，单位为秒
    config.set_default(connection_timeout=60)
    #设置私有space下载链接有效期,单位为秒
    config.set_default(expires=60)


# 设置日志文件

from ucloud import logger

locallogname = '' #完整本地日志文件名
logger.set_log_file(locallogname)
```

### 支持文件下载

  - demo程序



``` python
public_space = ''            #公共空间名称

private_space = ''            #私有空间名称

public_savefile = ''        #保存文件名

private_savefile = ''        #保存文件名

range_savefile = ''            #保存文件名

put_key = ''                #文件在空间中的名称

stream_key = ''                #文件在空间中的名称

from ucloud.uvideo import downloaduvideo

downloaduvideo_handler = downloaduvideo.DownloadUVideo(public_key, private_key)

# 从公共空间下载文件
ret, resp = downloaduvideo_handler.download_file(public_space, put_key, public_savefile, isprivate=False)
assert resp.status_code == 200

# 从私有空间下载文件

ret, resp = downloaduvideo_handler.download_file(private_space, put_key, private_savefile)
assert resp.status_code == 200

# 下载包含文件范围请求的文件

ret, resp = downloaduvideo_handler.download_file(public_space, put_key, range_savefile, isprivate=False, expires=300, content_range=(0, 50))
assert resp.status_code == 206
```

  - HTTP 返回状态码

| 状态码 | 描述           |
| --- | ------------ |
| 200 | 文件或者数据下载成功   |
| 206 | 文件或者数据范围下载成功 |
| 400 | 不存在的空间       |
| 403 | API公私钥错误     |
| 401 | 下载签名错误       |
| 404 | 下载文件或数据不存在   |
| 416 | 文件范围请求不合法    |

### 支持删除文件

  - demo程序



``` python
public_space = ''                #公共空间名称
private_bucekt = ''                #私有空间名称
delete_key = ''                    #文件在空间中的名称

from ucloud.uvideo import deleteuvideo

deleteuvideo_handler = deleteuvideo.DeleteUVideo(public_key, private_key)

# 删除公共空间的文件

ret, resp = deleteuvideo_handler.deletefile(public_space, delete_key)
assert resp.status_code == 204

# 删除私有空间的文件

ret, resp = deleteuvideo_handler.deletefile(private_space, delete_key)
assert resp.status_code == 204
```

  - HTTP 返回状态码

| 状态码 | 描述         |
| --- | ---------- |
| 204 | 文件或者数据删除成功 |
| 403 | API公私钥错误   |
| 401 | 签名错误       |

### 支持分片上传和断点续传

  - demo程序



``` python
public_space = ''        #公共空间名称
sharding_key = ''        #上传文件在空间中的名称
localfile = ''            #本地文件名

from ucloud.uvideo import multipartuploaduvideo

multipartuploaduvideo_handler = multipartuploaduvideo.MultipartUploadUVideo(public_key, private_key)

# 分片上传一个全新的文件

ret, resp = multipartuploaduvideo_handler.uploadfile(public_space, sharding_key, localfile)
while True:
if resp.status_code == 200: # 分片上传成功
    break
elif resp.status_code == -1:    # 网络连接问题，续传
    ret, resp = multipartuploaduvideo_handler.resumeuploadfile()
else:   # 服务或者客户端错误
    print(resp.error)
    break

# 分片上传一个全新的二进制数据流

from io import BytesIO
bio = BytesIO(u'你好'.encode('utf-8'))
ret, resp = multipartuploaduvideo_handler.uploadstream(public_space, sharding_key, bio)
while True:
if resp.status_code == 200:     # 分片上传成功
    break
elif resp.status_code == -1:    # 网络连接问题，续传
    ret, resp = multipartuploaduvideo_handler.resumeuploadstream()
else:   # 服务器或者客户端错误
    print(resp.error)
    break
```

  - HTTP 返回状态码

| 状态码 | 描述         |
| --- | ---------- |
| 200 | 文件或者数据上传成功 |
| 400 | 上传到不存在的空间  |
| 403 | API公私钥错误   |
| 401 | 上传凭证错误     |

### 空间管理

``` python
from ucloud.uvideo import spacemanager

spacemanager_handler = spacemanager.BucketManager(public_key, private_key)

# 创建新的space
spacename = '' #创建的空间名称
ret, resp = spacemanager.createspace(spacename, 'public')
assert resp.status_code == 200

# 删除space
spacename = '' #待删除的空间名称
ret, resp = spacemanager.deletespace(spacename)
print(ret)

# 获取space信息
spacename = '' # 待查询的空间名称
ret, resp = spacemanager.describespace(public_space)
print(ret)

# 更改space属性
spacename = '' # 待更改的私有空间名称
spacemanager.updatespace(spacename, 'public'):

# 获得空间文件列表
spacename = '' #待查询的空间名称
offset = 0      #文件列表起始位置
limit = 20      #获取文件数量
ret, resp = spacemanager.getfilelist(spacename, offset, limit)
print(ret)
```
