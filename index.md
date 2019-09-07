# 首页展示

## [ 描述 ]

用于统计平台累计接入车企总数，从大数据端获取数据后可直接展示

## [ Request ]

+ Request的构造主要由以下几个部分组成：
  + 请求行：
    + `GET /carPlat/index/queryData`
    + `GET /carPlat/index/manufacturerAndCount`
    + `GET /carPlat/index/periodAndCount`

  + Request Header：
    + `token : 7840c1d8014d3d352cdbe1614e30301d`

  + Request Body
    + 无

## [ Response ]

返回消息由返回状态行，HTTP头和消息体三部分组成:

+ HTTP Status Code  
`200 OK`

+ Response Header  
`Content-Type : application/json;charset=UTF-8`

+ Response Body返回的结果为JSON格式，车企的接入车数量按数量排序，返回前12个

``` json
{
    "code": 0,
    "msg": "success",
    "manufacturerSum": 33,
    "vehSum": 54421,
    "distanceSum": 198993222.60,
    "oilSaving": "7478.8",
    "carbonReduction": "16.6"
}

{
    "code": 0
    "msg": "success",
    "id": ["扬州亚星客车股份有限公司", "奇瑞新能源汽车股份有限公司","江西江铃集团新能源汽车有限公司"...],
    "value": [185,7...]
}

{
  "code": 0,
  "msg": "success",
  "id": ["00:00-02:00", "02:00-04:00", ...],
  "value": [
    [67, 15...]
  ]
}
```

注：code为0代表返回结果正常！
