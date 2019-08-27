# 各种类上线车辆

## [ 描述 ]

用于充电开始SOC剩余量对应累计充电次数 和 各车辆种类平均充电间隔

## [ Request ]

Request的构造主要由以下几个部分组成：

+ 请求行：
  + `GET /carPlat/runAnalysis/queryChargeNum/sum?startTime=2019-07-01&endTime=2019-07-31`
  + `GET /carPlat/runAnalysis/queryChargeNum/interval?startTime=2019-07-01&endTime=2019-07-31`
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
  "id": ["0-10%","10%-20%"...],
  "value": [197856, 656758...]
}

{
  "code": 0,
  "msg": "success",
  "id": ["私人车","租赁车"...],
  "value": [0.87, 0.3...]
}
```

注：code为0代表返回结果正常！
