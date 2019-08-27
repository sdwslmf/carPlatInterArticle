# 各种类上线车辆

## [ 描述 ]

用于各车辆种类次均充电时长 和 各车辆种类累计耗电量

## [ Request ]

Request的构造主要由以下几个部分组成：

+ 请求行：
  + `POST /carPlat/runAnalysis/queryChargeTimes/duration?startTime=2019-07-01&endTime=2019-07-31`
  + `POST /carPlat/runAnalysis/queryChargeTimes/consumption?startTime=2019-07-01&endTime=2019-07-31`
+ Request Header：
  + `token : 7840c1d8014d3d352cdbe1614e30301d`
  + Request Params  

参数名称|参数类型|是否必录入|说明
--|:--:|:--:|--
startTime | String | 是 | 查询条件的开始时间，默认为最新数据月份的第一天
endTime | String | 是 | 查询条件的结束时间，默认为最新数据月份的最后一天

## [ Response ]

返回消息由返回状态行，HTTP头和消息体三部分组成:

+ HTTP Status Code  
`200 OK`

+ Response Header  
`Content-Type : application/json;charset=UTF-8`

+ Response Body  
返回的结果为JSON格式

``` json
{
  "code": 0,
  "msg": "success",
  "id": ["私人车","租赁车"...],
  "value": [0.87, 0.3...]
}

{
  "code": 0,
  "msg": "success",
  "id": ["私人车","租赁车"...],
  "value": [197856, 656758...]
}
```

注：code为0代表返回结果正常！
