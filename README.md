# wl-address

#简介
  这是一个基于elementUi的el-select组件的省市县三级地址联动插件，使用本地化数据，无接口依赖。
  [el-select](https://element.eleme.cn/#/zh-CN/component/select)

## [在线演示](https://hql7.github.io/)

## 快速上手

`npm i wl-address --save`

或

`npm i wl-address -S`

`import wlAddress from 'wl-address'`

`Vue.use(wlAddress)`

### 使用
```
<template>
  <wlAddress class="my-wl-address" :type="address_mode" :address.sync="address_data"></wlAddress>
</template>  

<script>
export default {
  name: "app",
  data() {
    return {
      address_mode: "default", // default普通 cascader级联
      address_data: "" // 选中地址
    };
  },
  methods: {
    changeAddressMode() {
      this.address_mode =
        this.address_mode == "default" ? "cascader" : "default";
    }
  }
};
</script>
```

## 文档

  | 序号 | 参数 | 说明 | 类型 | 可选值 | 默认值 |
  | ---- | ---- | ---- | ---- | ---- | ---- |
  | 1 | size | 输入框尺寸 | String | medium/small/mini | - |
  | 2 | address | 绑定所选地址数据的字段。格式要求：[{"code":"130000","name":"河北省"},{"code":"130200","name":"唐山市"},{"code":"130203","name":"路北区"}] | String | - | - |
  | 3 | type | 三个下拉框联动模式和一个下拉框级联模式 | String |default/cascader| default |
  | 4 | disabled | 是否禁用 | Boolean | - | false |
  | 5 | clearable | 是否可清除选项 | Boolean | - | false |
  | 6 | filterable | 是否可搜索 | Boolean | - | false |
  | 7 | separator | cascader模式选项分隔符 | String | - | "/" |
  | 8 | showAllLevels | 输入框中是否显示选中值的完整路径 | Boolean | - | true |

## 版本记录

4. 0.2.3 增加一些配置参数，cascader模式时filterable无法触发筛选函数

3. 0.2.2 修复级联模式高度无限制的错误

2. 0.2.1 发布，增加为两个模式：三个下拉框联动模式和一个下拉框级联模式

1. 0.1.0 初次发布，0依赖的省市县三级地址插件

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
