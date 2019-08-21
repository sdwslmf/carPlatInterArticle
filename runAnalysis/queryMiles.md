# 各种类上线车辆

### &ensp;&ensp;[ 描述 ]

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;用于各车辆种类累积行驶里程 和 车辆日总行驶里程分布

### &ensp;&ensp;[ Request ]
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;Request的构造主要由以下几个部分组成：

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;请求行：

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;`POST /carPlat/runAnalysis/queryMiles?startTime=2019-07-01&endTime=2019-07-31`

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;Request Header：

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;`token : 7840c1d8014d3d352cdbe1614e30301d`

<<<<<<< HEAD
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;Request Param

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;Request Param 为 String 格式，说明如下：
=======
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;Request Params

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;Request Params说明如下：
>>>>>>> 157f78557a3bec82d2162d3350479afa22507370

参数名称|参数类型|是否必录入|说明
--|:--:|:--:|--
开始时间 | String | 否 | 查询条件的开始时间，默认为最新数据月份的第一天
结束时间 | String | 否 | 查询条件的结束时间，默认为最新数据月份的最后一天

<<<<<<< HEAD
=======

>>>>>>> 157f78557a3bec82d2162d3350479afa22507370
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
<<<<<<< HEAD
  "code": 0,
  "msg": "success",
  "bar": {
	"id": ["私人车","租赁车"...],
	"value": [67, 15...]
  },
  "barAndPie": {
	"id": [
			"0-20",
			"20-40",
			"40-60",
			"60-80",
			"80-100",
			"100-150",
			"150-200",
			"200-300",
			"300-400",
			"400-500",
			"500-600",
			"600-700",
			"700-800",
			"800-900",
			"900-1000",
			"1000及以上"
	],
	"value": [123, 400...]
  }
}
```

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;注：code为0代表返回结果正常！
=======
	"code": 0,
	"msg": success,
	"categoryAndDistance": {
		"id": ['公务', '公交', '环卫', '物流', '私人', '通勤', '租赁', '出租', '旅游'],
		"value": [7929048.4, 7112706.3, 3254.2, 1915417.0, 5616253.2, 206891.6, 16077467.3, 69179, 142582.8]
	},
	"distanceAndCount": {
		"id": ['0-20', '20-40', '40-60', '60-80', '80-100', '100-150', '150-200', '200-300', '300-400', '400-500', '500-600', '600-700', '700-800', '800-900', '900-1000', '1000及以上'],
		"value": [221095, 143133, 75275, 44743, 30450, 42544, 29237, 29499, 6951, 812, 207, 66, 20, 13, 10, 55]
	}
}

``
>>>>>>> 157f78557a3bec82d2162d3350479afa22507370
