# 各种类上线车辆

### &ensp;&ensp;[ 描述 ]

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;用于各车辆种类次均充电时长 和 各车辆种类累计耗电量

### &ensp;&ensp;[ Request ]
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;Request的构造主要由以下几个部分组成：

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;请求行：

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;`POST /carPlat/runAnalysis/queryChargeTimes?startTime=2019-07-01&endTime=2019-07-31`

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;Request Header：

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;`token : 7840c1d8014d3d352cdbe1614e30301d`

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;Request Param

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;Request Param 为 String 格式，说明如下：

参数名称|参数类型|是否必录入|说明
--|:--:|:--:|--
开始时间 | String | 否 | 查询条件的开始时间，默认为最新数据月份的第一天
结束时间 | String | 否 | 查询条件的结束时间，默认为最新数据月份的最后一天

### &ensp;&ensp;[ Response ]
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;返回消息由返回状态行，HTTP头和消息体三部分组成:

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;HTTP Status Code

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;`200 OK`

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;Response Header

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;`Content-Type : application/json;charset=UTF-8`

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;Response Body

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;返回的结果为JSON格式

``` json
{
  "code": 0,
  "msg": "success",
  "duration": {
	"id": ["私人车","租赁车"...],
	"value": [0.87, 0.3...]
  },
  "consumption": {
	"id": ["私人车","租赁车"...],
	"value": [197856, 656758...]
  }
}
```

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;注：code为0代表返回结果正常！
