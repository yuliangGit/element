<template>
  <div class="wrap">
    <ElDjSectionWrap v-for="(item,index) in list" :key="index" :title='`${title}${index+1}`'>
      <template slot="action">
        <el-button plain size="mini" icon="el-icon-arrow-up" :disabled="index<1"
                   @click="handleChangeListOrder(index-1,index)"></el-button>
        <el-button plain size="mini" icon="el-icon-arrow-down" :disabled="index>=list.length-1"
                   @click="handleChangeListOrder(index,index+1)"></el-button>
        <el-button plain size="mini" icon="el-icon-close" @click="handleDeleteCover(index)"></el-button>
      </template>
      <template slot="content">
        <slot name="item" :item="item" :index="index"></slot>
      </template>
    </ElDjSectionWrap>
    <el-button plain :class="`${anchorPoint} ${name}`" style="width: 100%" @click="handleAddCover"
               v-scrollJumpTo="{class:`${anchorPoint}`,index:0}">新建{{title}}
    </el-button>
  </div>
</template>
<script>
  import ElDjSectionWrap from 'element-ui/packages/dj-section-wrap';

  export default {
    name: 'ElDjSectionWrapWithMove',
    props: {
      name: {type: String, default: ''},
      list: {
        type: Array, default() {
          return [];
        }
      },
      title: {type: String, default: '模块'},
      max: {type: Number, default: 10}
    },
    data() {
      return {
        anchorPoint: `${this.name}_${new Date().getTime()}`
      };
    },
    components: {ElDjSectionWrap},
    methods: {
      handleChangeListOrder(i, j) {
        const temp = this.list[i];
        this.list[i] = this.list[j];
        // this.list[j] = temp; // $set为了让vue检测到数组的变化
        this.$set(this.list, j, temp);
      },
      handleDeleteCover(index) {
        this.list.splice(index, 1);
      },
      handleAddCover() {
        if (this.list.length <= this.max - 1) {
          this.list.push({});
        } else {
          this.$message({
            message: `最多添加${this.max}条`,
            type: 'warning'
          });
        }
      }
    }

  };
</script>
<style scoped lang="scss">
  .action {
    button {
      padding: 7px;
    }
  }
</style>


