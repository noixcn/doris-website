---
{
    "title": "PAD ROWSET",
    "language": "zh-CN"
}
---

# PAD ROWSET
## description
   
    该功能用于使用一个空的rowset填充损坏的副本。

    说明：这个功能暂时只在be服务中提供一个http接口。如果要使用，
    需要向要进行数据恢复的那台be机器的http端口发送pad rowset api请求。api格式如下：
    METHOD: POST
    URI: http://be_host:be_http_port/api/pad_rowset?tablet_id=xxx&start_version=xxx&end_version=xxx

## example

    curl -X POST "http://hostname:8088/api/pad_rowset?tablet_id=123456\&start_version=1111111\&end_version=1111112"

## keyword

    PAD,ROWSET,PAD,ROWSET
