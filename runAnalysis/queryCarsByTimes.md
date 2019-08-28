# 各时段上线车辆

## [ 描述 ]

用于不同种类各时段上线车辆情况

## [ Request ]

Request的构造主要由以下几个部分组成：

+ 请求行：
  + `GET /carPlat/runAnalysis/queryCarsByTimes?startDate=2019-07-01&endDate=2019-07-31`
  + `GET /carPlat/runAnalysis/seriesName?startDate=2019-07-01&endDate=2019-07-31`
+ Request Header：
  + `token : 7840c1d8014d3d352cdbe1614e30301d`
  + Request Params

参数名称|参数类型|是否必录入|说明
--|:--:|:--:|--
startDate | String | 是 | 查询条件的开始时间，默认为当前日期前推一个月对应日期
endDate | String | 是 | 查询条件的结束时间，默认为当前日期

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
  "id": ["0:00-2:00", "2:00-4:00", ...],
  "value": [
    [67, 15...], //私人车
    [25, 185...], //公务车
    [67, 15...], //租赁车
    [25, 185...], //出租车
    [67, 15...], //公交车
    [25, 185...], //旅游车
    [67, 15...], //通勤车
    [25, 185...], //公路车
    [67, 15...], //环卫车
    [25, 185...], //工程车
    [67, 15...], //邮政车
    [25, 185...], //物流车
  ]
}

{
  "code": 0,
  "msg": "success",
  "seriesName": ['私人车', '公务车', ...]
}
```

注：code为0代表返回结果正常！
