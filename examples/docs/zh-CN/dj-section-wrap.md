<script>
  export default {
      data(){
        return {
          data:{}
        }
      }
  };
</script>
<style scoped lang="scss">
</style>

## ElDjSectionWrap 到家模块外层样式

用来快速搭建中后台页面模块样式的组件

:::tip
其实我就是想测试一下把组件写在 ElementUI 的项目里面，成本是怎样的~ 规范是怎样的~
:::

### 正常使用

用户可以自己配置header、content区域的样式，内容

:::demo 这里应该是这个事例的一些介绍 比如`slot`

```html
<template>
  <el-dj-section-wrap title='文档管理' class="section-wrap--no-padding _doc-section">
    <template slot="action">
      <div class='sub_header'>
        <el-button>重置</el-button>
        <el-button>取消</el-button>
      </div>
    </template>
    <template slot="content">
        <el-form ref='detailManageForm' :model="data" :rules="detailFormRules" label-width="100px">
            <el-form-item label="服务概述" prop="">
              <el-input type="textarea" v-model.trim="description"></el-input>
            </el-form-item>
            <el-form-item label="背景图片" prop="photoUrl">
              <el-dj-img-upload
                v-model="photoUrl"
                action="/a/b/a"
                :accept="['image/jpeg','image/jpg','image/png']"
                :size="5*1024"
                imgWidthAndHeight="1920*340"
                exampleLink="//static.daojia.com/eife/djcloud-admin/dist/static/img/banner_details_1@2x.jpg"
                tipContent="图片内容在右侧，不影响左侧阅读。"
                :limit="1"></el-dj-img-upload>
            </el-form-item>
            <el-form-item label="按钮链接">
              <el-dj-btn-link-group ref="btnLink" v-model.trim="buttons" :max="5"></el-dj-btn-link-group>
            </el-form-item>
          </el-form>
    </template>
  </el-dj-section-wrap>
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

如果单独引入 `ElDjBtnLinkGroup`：

```javascript
import { ElDjBtnLinkGroup } from 'element-ui';
```


### Attributes

| 参数                     | 说明                             | 类型              | 可选值                           | 默认值               |
| ------------------------ | ------------------------------ | ----------------- | -------------------------------- | ------------------ |
| title                    | ElDjBtnLinkGroup 标题           | string           | —                                | —                  |
| headerStytle               | ElDjBtnLinkGroup 头部样式       | object            | -           |  {}  |
| contentStytle               | ElDjBtnLinkGroup 内容样式       | object            | -           |  {backgroundColor: '#F2F6FC'}  |


### Methods

| 方法名                     | 说明                           | 参数            |
| ------------------------ | ------------------------------ | ----------------- | 