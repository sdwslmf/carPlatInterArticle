# 数据接入

### &ensp;&ensp;[ 描述 ]

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;用于各类型统计车辆情况

### &ensp;&ensp;[ Request ]
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;Request的构造主要由以下几个部分组成：

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;请求行：

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;`GET /carPlat/dataAccess/queryData?startTime=2019-07-01&endTime=2019-07-31`

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;Request Header：


&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;`token : 7840c1d8014d3d352cdbe1614e30301d`

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;Request Params

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;Request Params说明如下：

参数名称|参数类型|是否必录入|说明
--|:--:|:--:|--
开始时间 | String | 否 | 查询条件的开始时间，默认为最早有数据的一天（2018-11-05）
结束时间 | String | 否 | 查询条件的结束时间，默认为当天



### &ensp;&ensp;[ Response ]
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;返回消息由返回状态行，HTTP头和消息体三部分组成:

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;HTTP Status Code

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;`200 OK`

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;Response Header

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;`Content-Type : application/json;charset=UTF-8`

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;Response Body

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;返回的结果为JSON格式，powerTypeAndCategory里的value第一个数组是纯电车辆数，第二个是混动车辆数

``` json
{
	"code": 0,
	"msg": "success",
	"vehCategory":{
		"id":["公务","公交","环卫","物流","私人","通勤","租赁","出租","旅游"],
		"value":[9451,2068,4,3046,8413,126,26374,19,40]
	},
	"powerTypeAndCount":{
		"id":["纯电动","混动"],
		"value":[48050,1491]
	},
	"powerTypeAndCategory":{
		"id":["通勤","物流","租赁","环卫","出租","公务","公交","旅游","私人"],
		"value":[
			[126,3046,26331,4,17,9388,1554,40,7544],
			[2,43,63,869,514,0,0,0,0]
		]
	}
}
```

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;注：code为0代表返回结果正常！
