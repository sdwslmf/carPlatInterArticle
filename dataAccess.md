# 数据接入

## [ 描述 ]

用于各类型统计车辆情况

## [ Request ]

+ Request的构造主要由以下几个部分组成：
  + 请求行：
    + `GET /carPlat/dataAccess/queryData/powerTypeAndCategory?startTime=2019-07-01&endTime=2019-07-31`
    + `GET /carPlat/dataAccess/queryData/powerTypeAndCount?startTime=2019-07-01&endTime=2019-07-31`
    + `GET /carPlat/dataAccess/queryData/vehCategory?startTime=2019-07-01&endTime=2019-07-31`
  + Request Header：
    + `token : 7840c1d8014d3d352cdbe1614e30301d`
    + Request Params

参数名称|参数类型|是否必录入|说明
--|:--:|:--:|--
startTime | String | 是 | 查询条件的开始时间，默认为2018-11-05
endTime | String | 是 | 查询条件的结束时间，默认为最新数据月份的最后一天

## [ Response ]

返回消息由返回状态行，HTTP头和消息体三部分组成:

+ HTTP Status Code  
`200 OK`

+ Response Header  
`Content-Type : application/json;charset=UTF-8`

+ Response Body
返回的结果为JSON格式，最后一个JSON里的value第一个数组是纯电车辆数，第二个是混动车辆数

``` json
{
  "code": 0,
  "msg": "success",
  "id":["通勤","物流","租赁","环卫","出租","公务","公交","旅游","私人"],
  "value":[
    [126,3046,26331,4,17,9388,1554,40,7544],
    [2,43,63,869,514,0,0,0,0]
  ]
}

{
  "code": 0,
  "msg": "success",
  "id":["纯电动","混动"],
  "value":[48050,1491]
}

{
  "code": 0,
  "msg": "success",
  "id":["公务","公交","环卫","物流","私人","通勤","租赁","出租","旅游"],
  "value":[9451,2068,4,3046,8413,126,26374,19,40]
}
```

注：code为0代表返回结果正常！
