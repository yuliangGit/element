<template>
  <div class="section-wrap">
    <el-row type="flex" align="middle" class="header" :style="headerStytle">
      <el-col :span="12">
        <span class="title">{{title}}</span>
      </el-col>
      <el-col :span="12" class="action">
        <slot name="action"></slot>
      </el-col>
    </el-row>
    <slot name="sub_header"></slot>
    <div class="content" :style="contentStytle">
      <slot name="content"></slot>
    </div>
  </div>
</template>
<script>
export default {
  name: 'ElDjSectionWrap',
  props: {
    title: { type: String, default: '' },
    headerStytle: {
      type: Object,
      default() {
        return {};
      }
    },
    contentStytle: {
      type: Object,
      default() {
        return { backgroundColor: '#F2F6FC' };
      }
    }
  }
};
</script>
<style scoped lang="scss">
.section-wrap {
  .header {
    padding: 10px 0;
    .title {
      padding-left: 10px;
      border-left: 5px solid #fa5967;
      color: #000000;
      font-size: 16px;
    }
    .action {
      text-align: right;
    }
  }
  .content {
    padding: 20px 40px;
    border: #ebeef5 1px solid;
  }
}
</style>


