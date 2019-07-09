# 回调说明

{{indexmenu_n>3}}

## 功能概述

视频转码、截图、切片、鉴黄等任务处理完成后，UMedia可以回调用户的接口，通知处理的结果。

客户需提供一个接收处理结果的URL地址，处理结果被封装成 json 字符串，通过 POST 请求，传递给用户的接口。

## 转码回调详情

使用带有“回调URL”的转码模版创建的转码任务完成后，UMedia会将处理结果传递到模版内所填写的回调地址。

详细参数如下：

    {
       "retcode":0, //0 表示处理成功，
       "task_id":"1", //提交转码生成的任务 id 
       "src_url":"http://src.ufile.ucloud.cn/my.mp4", //原始 url 地址 
       "dest_video_name":"my_720p.mp4", //目标文件名 
       "dest_video_url":"http://dest.ufile.ucloud.cn/my_720p.mp4", //目标文件地址
       "duration":587,//转码后 视频的时长，单位秒
       "file_size":587, //视频的文件大小
       "width":1280,//视频的宽，单位为像素
       "height":720, //视频的高，单位为像素
       "message":"succ" //处理结果描述
    }

## 截图回调详情

截图任务完成后，UMedia会将处理结果传递到创建该任务时所填写的回调地址。

详细参数如下:

    {
       "retcode":0, //0 表示处理成功，
       "task_id":"1", //提交截图生成的任务 id 
       "src_url":"http://src.ufile.ucloud.cn/my.mp4", //原始 url 地址 
       "image_count":3, //截图张数
       "image_list":[
           {"image_url":"http://dest.ufile.ucloud.cn/my_1.jpg"}, 
           {"image_url":"http:// dest.ufile.ucloud.cn/my_2.jpg"}, 
           {"image_url":"http://dest.ufile.ucloud.cn/my_3.jpg"}
       ],
       "message":"succ" //处理结果描述
    }

## 切片回调详情

切片任务完成后，UMedia会将处理结果传递到创建该任务时所填写的回调地址。

详细参数如下：

    {
       "retcode":0, //0 表示处理成功，
       "task_id":"1", //提交转码生成的任务 id 
       "src_url":"http://src.ufile.ucloud.cn/my.mp4", //原始 url 地址 
       "dest_video_name":"my.m3u8", //目标文件名 
       "dest_video_url":"http://dest.ufile.ucloud.cn/my.m3u8", //目标文件地址 
       "duration":587, //切片后视频的时长，单位秒
       "message":"succ" //处理结果描述
    }

## 鉴黄回调详情

UMedia当前通过API调用方式提供视频鉴黄服务。

鉴黄任务完成后，UMedia会将处理结果传递到调用API创建该任务时所填写的回调地址。

详细参数如下：

    {
       "retcode":0, //0 表示处理成功，
       "task_id":"1", //提交鉴黄生成的任务 id 
       "src_url":"http://src.ufile.ucloud.cn/my.mp4", //原始 url 地址 
       "image_count":5, //总的鉴黄图片张数
       "invalid_image_list":[ //有问题的图片列表
       {
           "name":" http://dest.ufile.ucloud.cn/my_1.jpg", //图片地址 
           "rate":0.9999947547912598, //该图片被识别为某个分类的概率值 
           "label":0, //图片分类，0 为色情，1 为性感，2 为正常
           "review":false //是否需要人工审核
       },
       {
           "name":" http://dest.ufile.ucloud.cn/my_2.jpg", 
           "rate":0.9999947547912598,
           "label":0,
           "review":false //是否需要人工审核
       }
       ],
       "message":"succ" //处理结果描述
    }
