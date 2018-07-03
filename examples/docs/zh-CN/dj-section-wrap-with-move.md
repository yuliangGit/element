<script>
  export default {
      data(){
        return {
          data:{},
          menus: [{}]
        }
      }
  };
</script>
<style scoped lang="scss">
  .sub_header{
    padding: 10px;
    background-color: #f8f8f8;
  }
</style>

## ElDjSectionWrapWithMove 到家模块外层样式可调换顺序

用来快速搭建中后台页面模块样式的组件

:::tip
其实我就是想测试一下把组件写在 ElementUI 的项目里面，成本是怎样的~ 规范是怎样的~
:::

### 正常使用

用户可以自己配置header、content区域的样式，内容

:::demo 这里应该是这个事例的一些介绍 比如`slot`

```html
<template>

<el-dj-section-wrap-with-move :min="1" :max="9" v-model="menus" headerBgc="#EBEEF5" contentBgc="#F2F6FC"
                                  title="页面">
  <template slot="item" slot-scope="{item,index}">
              我是第{{index}}个section wrap
  </template>
 </el-dj-section-wrap-with-move>

</template>
<script>
  export default {
    data(){
        return {
          arr:[{},{}]
        }
      },
    created(){
      this.$refs.demo.validate((valid)=>{
        console.log(valid)
      })
    },
    methods: {

    }
  }
</script>
<style lang="scss">
</style>
```
:::

:::tip
目前这个插件必须依赖于ElementUI 
:::

### 全局方法

如果你完整引入了 Element。 直接使用即可`<el-dj-btn-link-group  v-model="arr" :max="5" ></el-dj-btn-link-group>`

### 单独引用

如果单独引入 `ElDjSectionWrapWithMove`：

```javascript
import { ElDjSectionWrapWithMove } from 'element-ui';
```


### Attributes

| 参数                     | 说明                             | 类型              | 可选值                           | 默认值               |
| ------------------------ | ------------------------------ | ----------------- | -------------------------------- | ------------------ |
| title                    | ElDjBtnLinkGroup 标题           | string           | —                                | —                  |
| headerStytle               | ElDjBtnLinkGroup 头部样式       | object            | -           |  {}  |
| contentStytle               | ElDjBtnLinkGroup 内容样式       | object            | -           |  {backgroundColor: '#F2F6FC'}  |


### Slot

| 方法名                     | 说明                           | 参数            |
| ------------------------ | ------------------------------ | ----------------- | 
| action                   | hader右侧的区域为按钮区域，可以自定义添加功能 | - | 
| sub_header                | hader下方可以添加一行作为subheader | - | 
| content                   | 内容区域内容        | - | 