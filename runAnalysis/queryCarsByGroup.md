# 各种类上线车辆

## [ 描述 ]

用于各车辆种类日均车辆上线情况 和 各车辆种类车辆上线情况

## [ Request ]

Request的构造主要由以下几个部分组成：

+ 请求行：
  + `GET /carPlat/runAnalysis/queryCarsByGroup/avg?startDate=2019-07-01&endDate=2019-07-31`
  + `GET /carPlat/runAnalysis/queryCarsByGroup/sum?startDate=2019-07-01&endDate=2019-07-31`
+ Request Header：
  + `token : 7840c1d8014d3d352cdbe1614e30301d`
  + Request Params

参数名称|参数类型|是否必录入|说明
--|:--:|:--:|--
startDate | String | 是 | 查询条件的开始时间，默认为最新数据月份的第一天
endDate | String | 是 | 查询条件的结束时间，默认为最新数据月份的最后一天

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
  "id": ["公务","出租"...],
  "value": [67, 200...],
  "ratio": [1,20,30...] //上线率
}

{
  "code": 0,
  "msg": "success",
  "id": ["公务","出租"...],
  "value": [123, 400...],
  "ratio": [1,20,30...] //上线率
}
```

注：code为0代表返回结果正常！
