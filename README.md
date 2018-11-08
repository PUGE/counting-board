# notifications-puge

安装
```
npm i -save @puge/scoreboard
或
yarn add @puge/scoreboard
```

## 参数

| 参数        | 含义         | 类型  | 是否必须  |
| ----------- |:-------------:| -----:| -----:|
|num| 显示的数值 | Number | true |

## 动画样式
![default](http://p5qgrn52w.bkt.clouddn.com/counting-board/%E5%BD%95%E5%88%B6_2018_06_22_10_58_30_497.gif)

## 使用示例
```
<template>
  <div id="app">
    <counting :num="2323"></counting>
  </div>
</template>

<script>
import counting from '@puge/scoreboard'

export default {
  name: 'app',
  components: {
    counting
  }
}
</script>
```
