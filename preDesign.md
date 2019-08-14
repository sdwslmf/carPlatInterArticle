# 前端设计

## 技术栈

+ Vue/VueRouter/Vuex
+ axios（异步网络请求）
+ echarts（图表组件）
+ element UI（UI组件）
+ eslint（JavaScript代码检测工具）
+ webpack/gulp（自动构建工具）
+ scss（css扩展语言）

## 工程目录

```txt
├─build
├─config
├─node_modules
├─src
│  ├─assets
│  │  ├─img
│  │  └─scss
│  ├─components
│  │  ├─echarts
│  │  │  ├─bar
│  │  │  ├─bar-line
│  │  │  ├─bar-pie
│  │  │  └─pie
│  │  ├─icon-svg
│  │  └─table-tree-column
│  ├─element-ui
│  ├─element-ui-theme
│  ├─icons
│  │  └─svg
│  ├─mock
│  │  └─modules
│  ├─router
│  ├─store
│  │  └─modules
│  ├─utils
│  └─views
│      ├─common
│      ├─demo
│      └─modules
│          ├─charts
│          ├─job
│          ├─oss
│          └─sys
└─static
    ├─config
    ├─img
    ├─plugins
    │  ├─echarts-3.8.5
    │  ├─mock-1.0.0-beta3
    │  └─ueditor-1.4.3.3
    └─test
        ├─e2e
        │  ├─custom-assertions
        │  └─specs
        └─unit
            └─specs

```

## 路由设计

path: /src/router/index.js

+ 系统前端采用二级路由设计，第一级路由在根组件App.vue中，第二级路由在主页面组件main.vue下的main-content.vue中。
  + 一级路由主要作用为区分登录前页面login.vue（包含404页404.vue）和登录后主页面main.vue。
  + 二级路由主要根据路由连接在主页面main.vue中加载不同组件显示视图，只有主页面有二级路由。
  + 一级路由默认访问主页面main.vue，主页面二级路由默认访问home.vue，访问之前需要经过导航守卫的验证，导航守卫检测当前用户是否含有正确的token（身份验证采用token机制），验证通过则正常访问，失败则清除登录信息，跳转至登录页。
+ 所有的路由都要经过全局的导航守卫检测，如果要已获得动态路由或者要问登录页，则直接跳转，通过ajax请求向后端获取动态路由数据，并将获得到的数据添加至路由中，动态路由数据和权限数据将保存至sessionStorage中。
+ 组件加载默认使用Tabs方式，组件的URL以http(s)开头则使用iframe方式。
+ 路由对应的导航菜单如下：

```txt
├─首页
├─数据接入
└─运行分析
   ├─上线车辆
   │  ├─各类型上线车辆
   │  └─各种类上线车辆
   ├─行驶里程
   └─充/耗电
      ├─soc剩余量及充电间隔
      └─充电时长及耗电量

```

## 服务设计

path: src/utils

### 异步网络请求

path: src/utils/httpRequest.js

+ 异步网络请求采用axios实现，使用自定义配置新建一个axios实例，配置内容为超时时间为30秒，网络请求带上cookie以及设置请求头。
+ 请求拦截设置，在请求头上添加token。
+ 响应拦截设置，如果token失效则清除登录信息并跳转至登录页。
+ 开发时环境在开启代理的情况下将使用代理设置进行跨域，生产时环境直接请求window.SITE_CONFIG.baseUrl
+ get和post请求添加默认参数设置，默认参数为当前时间戳。
+ axios实例将作为Vue的一个属性http挂在到全局，在组件中无需导入可以直接使用该方法。

### 其他服务

path: src/utils/index.js, src/utils/validate.js

包含生成uuid、获取权限、清除登录信息、树形数据转换、数据验证等工具函数，在组件中使用需要进行导入。

## 组件设计

### 图表组件设计

设计四种图表组件，包括[饼图组件](https://echarts.baidu.com/examples/editor.html?c=pie-legend)、[柱状图组件](https://echarts.baidu.com/examples/editor.html?c=bar-tick-align)、[柱状图+饼图组件](https://echarts.baidu.com/examples/editor.html?c=mix-timeline-finance)、[柱状图+折线图组件](https://echarts.baidu.com/examples/editor.html?c=mix-line-bar)，这些组件存放于src/components/echarts/下，目录结构：

```txt
src/components/echarts/
├─bar
│      bar.vue
│      option.js
│
├─bar-line
│      bar-line.vue
│      option.js
│
├─bar-pie
│      bar-pie.vue
│      option.js
│
└─pie
        pie.vue
        option.js
```

+ 每个图表组件独占一个目录，目录下含有vue单文件组件和echarts配置项options.js。
+ option.js内导出一个配置对象以供单文件组件使用，包含基本配置信息（展示的数据除外）。
+ 每单文件组件含有prop数据接口，用于获取父组件传递来的所要展示的数据，单文件组件负责将这些数据加入到配置对象中，并以此为依据渲染视图。
+ 单文件组件内采用ref的方式获取子组件或元素。

## 页面设计

path: src/views

### 登录页login.vue

path: src/views/common/login.vue

+ 页面布局  
  + login.vue采用左右布局，左侧为登录页图片，右侧为表单域。
  + 表单域内含有账户、密码、验证码三项文本输入框和一项登录按钮
  + 表单域使用element UI组件。
+ 表单验证  
表单验证采用element UI组件提供的validate方法，在表单验证通过后才能进行身份验证。
+ 身份验证  
  + 登录前login.vue提供uuid向后端服务器发起Ajax请求获取对应的验证码。
  + 在前端表单验证通过后将账户、密码、uuid以及验证码发送到后端进行身份验证。
  + 若验证成功，将后端发送的token存入cookie中，并发起路由跳转跳转到主页面中；若失败，将提示错误信息并重新生成uuid请求新的验证码，并重复上述过程。

### 主页面main.vue

path: src/views/main.vue

+ 页面布局
  + 主页面采用定位布局的方式实现，包含main-navbar.vue、main-sidebar以及main-content.vue组件。
  + main-navbar显示当前用户和系统主题的相关信息。
  + main-sidebar.vue组件包含所有的二级路由连接。
  + 由二级路由加载的视图将在main-content组件中显示。
+ 路由链接写入
  + main-sidebar.vue在初始化过程中读取sessionStorage中有关动态路由和权限的相关数据写入状态管理中，将符合当前用户的路由链接显示出来。

### 首页home.vue（一级菜单）

path: src/views/home.vue

+ 以数字的形式展示截至目前的累计接入车企数、车辆总数，累计行驶里程数/在青行驶里程数，节油量、碳减排。
+ 采用定位布局的方式对展示的数字进行布局。
+ 使用Vue的http属性向后端获取以上数据，请求地址为`/index/queryData`，数据格式为

```JavaScript
{
  enterpriseSum: number,
  carSum: number,
  distanceSum: number,
  distanceQD: number,
  oilSaving: number,
  carbonReduction: number
}
```

### 数据接入data-access.vue（一级菜单）

path: src/views/charts/data-access.vue

+ 页面布局
  + 该页面共3个图，分上下两行展示，采用定位布局实现  
  + 第一行：“车辆种类统计”（柱状图加饼图）及“动力类型统计”（饼图）  
  + 第二行：“车辆种类对应动力类型”（柱状图）  
  + 页面包含日期选择器，起止日期作为查询参数。

+ 数据获取  
组件使用封装在Vue里的http服务向后端获取数据，请求地址为`/sjjr/queryData`，数据格式为

```JavaScript
{
  carType: {  // 根据 value 值降序排列
    id: Array<string>,
    value: Array<number>
  },
  dynamicType: {
    id: Array<string>,
    value: Array<number>
  },
  carAndDynamic: {
    electric: {
      id: Array<string>,
      value: Array<number>
    },
    mix: {
      id: Array<string>,
      value: Array<number>
    }
  }
}
```

+ 图表渲染  
获取到响应数据后，将每张图的数据通过prop的方式传入相应的图表组件中，以进行视图渲染。

### 各种类上线车辆页面online-type.vue（三级菜单）

path: src/views/charts/online-type.vue

+ 页面布局
  + 该页面共2个图，分上下两行展示。  
  + 第一行：“各种类日均车辆上线情况”（柱状图+折线图）  
  + 第二行：“各种类车辆上线情况”（柱状图+折线图）  
  + 页面包含日期选择器，起止日期作为查询参数。

+ 数据获取
组件使用封装在Vue里的http服务向后端获取数据，请求地址为`/yxfx/queryCarsByGroup`，数据格式为

```JavaScript
{
  avg: {
    id: Array<string>,
    value: Array<number>
  },
  sum: {
    id: Array<string>,
    value: Array<number>
  }
}
```

+ 图表渲染  
获取到响应数据后，将每张图的数据通过prop的方式传入相应的图表组件中，以进行视图渲染。

### 各时段上线车辆online-hour.vue（三级菜单）

path: src/views/charts/online-hour.vue

+ 页面布局
  + 使用柱状图展示每个车辆种类的上线情况进行分时段统计。
  + 各图标题备注车辆种类。
  + 页面包含日期选择器，起止日期作为查询参数。

+ 数据获取  
组件使用封装在Vue里的http服务向后端获取数据，请求地址为`/yxfx/queryCarsByTimes`，数据格式为

```JavaScript
{
  privateCar: {
    id: Array<string>,
    value: Array<number>
  },
  LeasedCar: {
    id: Array<string>,
    value: Array<number>
  },
  dienstwagen: {
    id: Array<string>,
    value: Array<number>
  },
  taxi:{
    id: Array<string>,
    value: Array<number>
  },
  bus: {
    id: Array<string>,
    value: Array<number>
  },
  touringCar: {
    id: Array<string>,
    value: Array<number>
  },
  commuterCar: {
    id: Array<string>,
    value: Array<number>
  },
  roadVehicle: {
    id: Array<string>,
    value: Array<number>
  },
  sanitatioTruck: {
    id: Array<string>,
    value: Array<number>
  },
  constructionVehicle: {
    id: Array<string>,
    value: Array<number>
  },
  postalCar: {
    id: Array<string>,
    value: Array<number>
  },
  logisticsVehicle: {
    id: Array<string>,
    value: Array<number>
  }
}
```

+ 图表渲染  
获取到响应数据后，将每张图的数据通过prop的方式传入相应的图表组件中，以进行视图渲染。

### 行驶里程distance.vue（二级菜单）

path: src/views/charts/distance.vue

+ 页面布局
  + 共2个图，左右两列展示。
  + 第一列：“各种类车辆累积行驶里程”（柱状图）。
  + 第二列：“车辆日总行驶里程分布”（柱状图+饼状图）。
  + 页面包含日期选择器，起止日期作为查询参数。

+ 数据获取  
组件使用封装在Vue里的http服务向后端获取数据，请求地址为`/yxfx/queryMiles`，数据格式为

```JavaScript
{
  bar: {
    id: Array<string>,
    value: Array<number>
  },
  barAndPie: {
    id: Array<string>,
    value: Array<number>
  }
}
```

+ 图表渲染  
获取到响应数据后，将每张图的数据通过prop的方式传入相应的图表组件中，以进行视图渲染。

### soc剩余量及充电间隔soc.vue（三级菜单）

path: src/views/charts/soc.vue

+ 页面布局
  + 共2个图，分上下两行展示；
  + 第一行：“充电开始SOC剩余量对应累计充电次数”（柱状图）；
  + 第二行：“各种类车辆平均充电间隔”（柱状图）；
  + 页面包含日期选择器，起止日期作为查询参数。

+数据获取  
组件使用封装在Vue里的http服务向后端获取数据，请求地址为`/yxfx/queryChargeNum`，数据格式为

```JavaScript
{
  sum: {
    id: Array<string>,
    value: Array<number>
  },
  internal: {
    id: Array<string>,
    value: Array<number>
  }
}
```

+ 图表渲染
获取到响应数据后，将每张图的数据通过prop的方式传入相应的图表组件中，以进行视图渲染。

### 充电时长及耗电量charge.vue（三级菜单）

path: src/views/charts/charge.vue

+ 页面布局
  + 共2个图，分上下两行展示；
  + 第一行：“各车辆种类次均充电时长”（柱状图）；
  + 第二行：“各车辆种类累计耗电量”（柱状图）；
  + 页面包含日期选择器，起止日期作为查询参数。

+ 数据获取  
组件使用封装在Vue里的http服务向后端获取数据，请求地址为`/yxfx/queryChargeTimes`，数据格式为

```JavaScript
{
  duration: {
    id: Array<string>,
    value: Array<number>
  },
  consumption: {
    id: Array<string>,
    value: Array<number>
  }
}
```

+ 图表渲染
获取到响应数据后，将每张图的数据通过prop的方式传入相应的图表组件中，以进行视图渲染。

## eslint配置

+ 禁用var声明（error）
+ const声明优先（error）
+ 每条语句必须使用结束符（error）
+ 禁止未使用过的表达式（error）
+ 要求使用 === 和 !==（error）
+ 禁止未使用过的变量（error）
+ 代码缩进使用两个空格（warn）
+ JavaScript字符串使用单引号（warn）
+ 在文件末尾加入空行
