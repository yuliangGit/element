<script>
  export default {
      data(){
        return {
          arr:[{}]
        }
      }
  };
</script>

## ElDjBtnLinkGroup 到家链接按钮组

用来自定义按钮样式、名称、跳转链接的组件

:::tip
其实我就是想测试一下把组件写在 ElementUI 的项目里面，成本是怎样的~ 规范是怎样的~
:::

### 添加按钮

用户可以自有添加删除。可以配置最大添加几条

:::demo 这里应该是这个事例的一些介绍 比如`:max="5"`

```html
<template>
  <el-dj-btn-link-group  v-model.tirm="arr" :max="5" ></el-dj-btn-link-group>
</template>
<script>
  export default {
    data(){
        return {
          arr:[{},{}]
        }
      },
    methods: {

    }
  }
</script>
```

:::

:::tip
目前这个插件必须依赖于ElementUI 因为一些错误方法，直接调用了message。
想法是，运营后台类项目，直接全局使用ElementUI
:::

### 全局方法

如果你完整引入了 Element。 直接使用即可`<el-dj-btn-link-group  v-model="arr" :max="5" ></el-dj-btn-link-group>`

### 单独引用

如果单独引入 `ElDjBtnLinkGroup`：

```javascript
import { ElDjBtnLinkGroup } from 'element-ui';
```


### Options

| 参数                     | 说明                                                                                               | 类型                                                                                                                                                             | 可选值                           | 默认值                                          |
| ------------------------ | -------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------- | ----------------------------------------------- |
| model                    | ElDjBtnLinkGroup 值                                                                                    | arry                                                                                                                                                           | —                                | —                                               |
| max                   | ElDjBtnLinkGroup 最大个数                   | number              | -           |  5  |