<template>
  <div class="dj-img-upload--write">
    <span class="img-tip">图片尺寸{{this.imgWidthAndHeight}}，格式为{{this.acceptMessage}}，大小不超过{{this.size /
        1024}}M。{{tipContent}}下载 <a :href="exampleLink"
                                    target="_blank">[样例]</a></span>
    <el-upload
      :action="action"
      list-type="picture-card"
      :on-preview="handlePictureCardPreview"
      :on-remove="handleRemove"
      :on-change="handleChange"
      :on-success="handleSuccess"
      :file-list="list"
      :before-upload="beforeImgUpload"
      :class="{'is-hide':list.length>=limit}"
      :limit="limit">
      <i class="el-icon-plus"></i>
    </el-upload>
    <el-dialog :visible.sync="dialogVisible">
      <img width="100%" :src="dialogImageUrl" alt="">
    </el-dialog>
  </div>
</template>
<script>
  import emitter from 'element-ui/lib/mixins/emitter';

  export default {
    name: 'ElDjImgUpload',
    props: {
      value: {
        type: Array, default() {
          return [];
        }
      },
      action: {type: String, default: ''},
      limit: {type: Number, default: 1},
      accept: {
        type: Array, default() {
          return [];
        }
      },
      size: {type: Number, default: 3 * 1024},
      imgWidthAndHeight: {type: String, default: '200*100'},
      tipContent: {type: String, default: ''},
      exampleLink: {type: String, default: ''}
    },
    // list变化时，同步到父类的v-model上
    watch: {
      // list() {
      //   this.updateValue();
      // },
      value() {
        this.list = this.value;
      }
    },
    mixins: [emitter],
    created() {
      this.updateValue();
    },
    data() {
      return {
        dialogImageUrl: '',
        dialogVisible: false,
        list: this.value,
        errMessage: `图片格式有误，请上传尺寸${this.imgWidthAndHeight}，大小不超过${this.size /
        1024}M的${this.accept.join('、')}文件。`,
        acceptMessage: this.transformAcceptMessage()
      };
    },
    methods: {
      handleRemove(file, fileList) {
        console.log('handleRemove', file, fileList);
        this.list = fileList;
        this.updateValue();
      },
      handlePictureCardPreview(file) {
        this.dialogImageUrl = file.url;
        this.dialogVisible = true;
      },
      handleChange(file, fileList) {
        console.log('change', file, fileList);
      },
      handleSuccess(response, file, fileList) {
        console.log('handleSuccess', response, file, fileList);
        const l = fileList.length;
        const _arr = fileList;
        for (let i = 0; i < l; i++) {
          _arr[i].url = _arr[i].response.data;
        }
        console.log('change', file, fileList);
        this.list = _arr;
        this.updateValue();
      },
      beforeImgUpload(file) {
        // 检验图片格式
        if (this.accept.indexOf(file.type) < 0) {
          this.$message({
            message: this.errMessage,
            type: 'error'
          });
          return false;
        }
        // 检验图片大小
        if (file.size > this.size * 1024) {
          this.$message({
            message: this.errMessage,
            type: 'error'
          });
          return false;
        }
      },
      updateValue() {
        // const arr = this.list.map(item => ({url: item.url}));
        // 更新组件v-model的数据
        this.$emit('input', this.list);
        // 触发表表验证
        this.dispatch('ElFormItem', 'el.form.change', [this.list]);
      },
      transformAcceptMessage() {
        const arr = this.accept;
        const l = arr.length;
        let arrMessage = '';
        for (let i = 0; i < l; i++) {
          arrMessage = arrMessage + arr[i].split('/')[1] + '、';
        }
        arrMessage = arrMessage.substring(0, arrMessage.length - 1);
        return arrMessage;
      }
    }
  };
</script>
<style lang="scss">
  /*由于需要复写el组件样式，此处去除了css作用域，用dj-img-upload--rewrite格式*/
  .dj-img-upload--write {
    overflow: hidden;
    .img-tip {
      color: #C0C4CC;
      font-size: 14px;
      a {
        color: #409EFF;
      }
    }
    .is-hide {
      margin-bottom: 5px;
      .el-upload--picture-card {
        display: none;
      }
      > ul li {
        float: left;
      }
    }
  }
</style>


