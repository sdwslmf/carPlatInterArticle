# 各种类上线车辆

### &ensp;&ensp;[ 描述 ]

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;用于各车辆种类累积行驶里程 和 车辆日总行驶里程分布

### &ensp;&ensp;[ Request ]
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;Request的构造主要由以下几个部分组成：

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;请求行：

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;`GET /carPlat/runAnalysis/queryMiles?startTime=2019-07-01&endTime=2019-07-31`

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;Request Header：

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;`token : 7840c1d8014d3d352cdbe1614e30301d`

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;Request Params

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;Request Params说明如下：

参数名称|参数类型|是否必录入|说明
--|:--:|:--:|--
<<<<<<< HEAD
开始时间 | String | 否 | 查询条件的开始时间，默认为2018-11-05
结束时间 | String | 否 | 查询条件的结束时间，默认为最新一天
=======
startTime | String | 否 | 查询条件的开始时间，默认为最新数据月份的第一天
endTime | String | 否 | 查询条件的结束时间，默认为最新数据月份的最后一天
>>>>>>> fad920e9630102f1ab9b902d3924eeb3d62b1e9b


### &ensp;&ensp;[ Response ]
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;返回消息由返回状态行，HTTP头和消息体三部分组成:

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;HTTP Status Code

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;`200 OK`

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;Response Header

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;`Content-Type : application/json;charset=UTF-8`

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;Response Body

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;返回的结果为JSON格式，里程数从大到小排序，没有里程的种类不会出现

``` json
{
    "msg": "success",
    "code": 0,
    "categoryAndDistance": {
        "id":['租赁', '公务', '公交', '私人', '出租', '物流', '旅游', '通勤', '环卫'],
        "value":[17207311.2, 12748013.4, 7407762.0, 6999025.9, 2521133, 1936469.8, 150101.9, 82341.0, 3337.1]
    },
    "distanceAndCount": {
        "id": ['0-20', '20-40', '40-60', '60-80', '80-100', '100-150', '150-200', '200-300', '300-400', '400-500', '500-600', '600-700', '700-800', '800-900', '900-1000', '1000及以上']
        "value": [227001, 153893, 85895, 53595, 37410, 52343, 34717, 47850, 13881, 1494, 230, 70, 32, 14, 7, 66]
    }
}
```

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;注：code为0代表返回结果正常！
