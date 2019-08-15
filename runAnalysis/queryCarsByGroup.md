# 各种类上线车辆

### &ensp;&ensp;[ 描述 ]

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;用于各车辆种类日均车辆上线情况 和 各车辆种类车辆上线情况

### &ensp;&ensp;[ Request ]
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;Request的构造主要由以下几个部分组成：

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;请求行：

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;`POST /carPlat/yxfx/queryCarsByGroup`

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;Request Header：

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;`Content-Type : application/json;charset=UTF-8`

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;`token : 7840c1d8014d3d352cdbe1614e30301d`

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;Request Body

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;Request Body 为 JSON 格式，说明如下：

参数名称|参数类型|是否必录入|说明
--|:--:|:--:|--
开始时间 | String | 否 | 查询条件的开始时间，默认为最新数据月份的第一天
结束时间 | String | 否 | 查询条件的结束时间，默认为最新数据月份的最后一天

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;示例参数:

``` json
{
        "startTime": "2019-07-01",
        "endTime": "2019-07-31"
}
```

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
  "avg": {
	"id": ["公务","出租"...],
	"value": [67, 200...],
  "ratio": [1,20,30...] //上线率
  },
  "sum": {
	"id": ["公务","出租"...],
	"value": [123, 400...],
  "ratio": [1,20,30...] //上线率
  }
}
```