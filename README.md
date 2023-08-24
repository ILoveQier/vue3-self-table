<!--
 * @Description: vue3+elementplus 组件库
 * @Author: wangchao123
 * @Date: 2022-09-30 14:51:14
-->

# vue3+elementplus 组件库

## 如何运行

> 参考地址：https://git-scm.com/book/zh/v2/Git-%E5%B7%A5%E5%85%B7-%E5%AD%90%E6%A8%A1%E5%9D%97

1. 如果项目中有子模块了: git submodule init
2. 拉取到本地子模块： git submodule add http://gitlab.babec.com/baec-cli/vue3-tools.git

## 配合技术

- vite 插件
- vue3+elementplus

## MyTable 组件使用规则

> import MyTable from '@v3c/MyTable';

1. 基本使用

```vue
<MyTable :option="tableOption" ref="myTableRef"></MyTable>
<script setup>
  const tableOption = ref({
    columns: [
      { property: 'carNumber', label: '车牌号' },
      { property: 'driverName', label: '驾驶员姓名' },
      { property: 'workBegin', label: '排班开始时间' },
      { property: 'workEnd', label: '排班结束时间' },
    ],
  })
</script>
```

2. 常用配置

### 2.1 组件配置选项

| 参数 | 说明 | 子项说明 | 类型 | 可选值 | 默认值 | 描述 |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| isSelection | 首列是否显示多选框 | —— | boolean | true | false | —— |
| isBorder | 是否显示边框 | —— | boolean | true | false | —— |
| hlcr | 当前选中行是否高亮 | —— | boolean | true | false | —— |
| isIndex | 是否显示序号列 | —— | boolean | true | false | —— |
| columns | 表格列字段配置 | —— | array | —— | [] | 必选，每列必须配置 property 和 label 属性 |
|  | property | 列数据字段 | string | —— | —— | 必选 |
|  | label | 列名称 | string | —— | —— | 必选 |
|  | width | 列宽度 | number/string | number / number + "px" | "auto" | 可选，"auto" 或 数字或数字+"px" |
|  | type | 列类型 | string | "opt" | ——— | 可选，当 type 为"opt",模板中可以定义一个或多个插槽，插槽名格式为：`#opt-${property}` |
|  | tipType | 溢出文本提示框类型 | string | "toolTip"/"windowFixed" | "" | tipType 为 toolTip 时，使用的是 el-popover 自带提示框，tipType 为"windowFixed"时，使用的是自定义的提示窗 |
| request | 接口配置 | —— | object | —— | —— | 可选，当配置 request 字段时，必须配置 api 和 apiUrl 属性 |
|  | api | 请求公共部分配置 | object | —— | —— | 必选，统一封装 request 请求 |
|  | apiUrl | 接口地址 | string |  |  | 必选 |
|  | apiMethod | 请求方式 | string | "POST"/"GET" | "GET" | 可选 |
|  | apiData | 请求参数 | object | —— | {} | 请求接口所需参数 |
|  | postObj | 数据和总条数字段 | object | —— | { data: "data", total: "total" } | 指定组件使用接口返回的数据和总条数字段 |
| pagination | 分页组件配置 | —— | object | —— | —— | 可选，配置此项表示表格带分页 |
|  | footerStyle | 分页组件样式 | object |  |  | 可选，控制分页组件外层样式 |
|  | pageSize | 每页条数 | number | —— | 5 | 可选 |
|  | numName | 请求接口页数字段 | string | —— | "pageNum" | 自定义请求接口对应的页数字段 |
|  | sizeName | 请求接口每页条数字段 | string | —— | "pageSize" | 自定义请求接口对应的每页条数字段 |
|  | layout | 分页子组件 | string | "total,prev,pager,next,jumper" | "total,prev,pager,next,jumper" | 一般可以只配置 "prev,pager,next" |

### 2.2 基础项样式配置

```vue
<MyTable :option="tableOption" ref="myTableRef"></MyTable>
<script setup>
  const tableOption = ref({
    isSelection: true,
    isBorder: true,
    hlcr: true,
    isIndex: true,
    columns: [
      {
        { property: 'carNumber', label: '车牌号' },
        { property: 'driverName', label: '驾驶员姓名'},
        { property: 'workBegin', label: '排班开始时间'},
        { property: 'workEnd', label: '排班结束时间' }
      }
    ]
  })
</script>
```

### 2.3 表格列字段配置(columns)

```vue
<MyTable :option="tableOption" ref="myTableRef"></MyTable>
<script setup>
  const tableOption = ref({
    isSelection: true,
    isBorder: true,
    hlcr: true,
    isIndex: true,
    columns: [
      { property: 'carNumber', label: '车牌号', width: 100 },
      { property: 'driverName', label: '驾驶员姓名', width: 200 },
      { property: 'workBegin', label: '排班开始时间', width: '100px' },
      { property: 'workEnd', label: '排班结束时间', width: 'auto' },
    ],
  })
</script>
```

### 2.3 接口配置(request)

```vue
<MyTable :option="tableOption" ref="myTableRef"></MyTable>
<script setup>
  import request from '@/utils/request'
  const tableOption = ref({
    isSelection: true,
    isBorder: true,
    hlcr: true,
    isIndex: true,
    columns: [
      { property: 'carNumber', label: '车牌号', width: 100 },
      { property: 'driverName', label: '驾驶员姓名', width: 200 },
      { property: 'workBegin', label: '排班开始时间', width: 100 },
      { property: 'workEnd', label: '排班结束时间', width: 100 },
    ],
    request: {
      api: request,
      apiUrl: '/web/v2.2/workSchedule/page',
      apiMethod: 'POST', // 可选
    },
  })
</script>
```

### 2.4 分页参数配置(pagination)

```vue
<MyTable :option="tableOption" ref="myTableRef"></MyTable>
<script setup>
  import request from '@/utils/request'
  const tableOption = ref({
    isSelection: true,
    isBorder: true,
    hlcr: true,
    isIndex: true,
    columns: [
      { property: 'carNumber', label: '车牌号', width: 100 },
      { property: 'driverName', label: '驾驶员姓名', width: 200 },
      { property: 'workBegin', label: '排班开始时间', width: 100 },
      { property: 'workEnd', label: '排班结束时间', width: 100 },
    ],
    request: {
      api: request,
      apiUrl: '/web/v2.2/workSchedule/page',
      apiMethod: 'POST',
    },
    pagination: {
      pageSize: 10,
    },
  })
</script>
```

3. 高级用法

### 3.1 表格列字段配置(columns)

```vue
<MyTable :option="tableOption" ref="myTableRef">
  <template #opt-check="{ scope }">
    <el-button type="danger">查看</el-button>
  </template>
   <template #opt-reset="{ scope }">
    <el-button type="danger">删除</el-button>
  </template>
</MyTable>
<script setup>
  import request from '@/utils/request'
  const tableOption = ref({
    isSelection: true,
    isBorder: true,
    hlcr: true,
    isIndex: true,
    columns: [
      { property: 'carNumber', label: '车牌号', width: 100 },
      { property: 'driverName', label: '驾驶员姓名', width: 200, tipType: 'toolTip' },
      { property: 'workBegin', label: '排班开始时间', width: '100px', tipType: 'windowFixed' },
      { property: 'workEnd', label: '排班结束时间', width: 'auto' },
      { property: 'check', label: '查看', type: 'opt' },
      { property: 'reset', label: '重置', type: 'opt' },
    ],
  })
</script>
```

### 3.2 接口配置(request)

```vue
<MyTable :option="tableOption" ref="myTableRef"></MyTable>
<script setup>
  const tableOption = ref({
    isSelection: true,
    isBorder: true,
    hlcr: true,
    isIndex: true,
    columns: [
      { property: 'carNumber', label: '车牌号', width: 100 },
      { property: 'driverName', label: '驾驶员姓名', width: 200 },
      { property: 'workBegin', label: '排班开始时间', width: 100 },
      { property: 'workEnd', label: '排班结束时间', width: 100 },
    ],
    request: {
      api: request,
      apiUrl: '/web/v2.2/workSchedule/page',
      apiMethod: 'POST',
      postObj: { data: 'data.rows', total: 'data.total' },
    },
  })
</script>
```

### 3.3 分页参数配置(pagination)

```vue
<MyTable :option="tableOption" ref="myTableRef"></MyTable>
<script setup>
  const tableOption = ref({
    isSelection: true,
    isBorder: true,
    hlcr: true,
    isIndex: true,
    columns: [
      { property: 'carNumber', label: '车牌号', width: 100 },
      { property: 'driverName', label: '驾驶员姓名', width: 200 },
      { property: 'workBegin', label: '排班开始时间', width: 100 },
      { property: 'workEnd', label: '排班结束时间', width: 100 },
    ],
    request: {
      api: request,
      apiUrl: '/web/v2.2/workSchedule/page',
      apiMethod: 'POST',
      postObj: { data: 'data.rows', total: 'data.total' },
    },
    pagination: {
      footerStyle: {
        margin: '10px 0',
        float: 'right',
      },
      pageSize: 10,
      numName: 'pageNum', // 可选
      sizeName: 'pageSize', // 可选
      layout: 'total,prev, pager, next, jumper',
    },
  })
</script>
```

4. 较完整的例子

```vue
<MyTable :option="tableOption" ref="myTableRef">
  <template #opt-check="{ scope }">
    <el-button type="danger" @click="checkDriver(scope)">查看</el-button>
  </template>
  <template #opt-reset="{ scope }">
    <el-button type="danger" @click="resetDriver(scope)">重置</el-button>
  </template>
</MyTable>
<script setup>
  import request from '@/utils/request'
  const tableOption = ref({
    isSelection: true,
    isBorder: true,
    hlcr: true,
    isIndex: true,
    columns: [
      { property: 'carNumber', label: '车牌号', width: 100 },
      { property: 'driverName', label: '驾驶员姓名', width: 200, tipType: 'windowFixed' },
      { property: 'workBegin', label: '排班开始时间', width: '100px' },
      { property: 'workEnd', label: '排班结束时间', width: 'auto' },
      { property: 'opt', label: '操作', type: 'opt' },
    ],
    request: {
      api: request,
      apiUrl: '/web/v2.2/workSchedule/page',
      apiMethod: 'POST',
      apiData,
      postObj: { data: 'data.rows', total: 'data.total' },
    },
    pagination: {
      footerStyle: {
        margin: '10px 0',
        float: 'right',
      },
      pageSize: 10,
      numName: 'pageNum', // 可选
      sizeName: 'pageSize', // 可选
    },
  })
  function checkDriver(scope) {
    console.log(scope)
  }
  function resetDriver(scope) {
    console.log(scope)
  }
</script>
```

## MyForm 组件使用规则

```
import MyForm from '@v3c/MyForm';
```
