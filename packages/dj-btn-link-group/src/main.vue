<template>
  <div class="_dj_btn_link_group">
    <el-form v-if="btnArr.length>0" class="_form" :model="dynamicValidateForm" ref="dynamicValidateForm"
             label-width="80px">
      <el-row class="row" v-for="(item, index) in dynamicValidateForm.list" :key="index">
        <el-col :span="6">
          <el-form-item
            label="按钮文字"
            :prop="'list.' + index + '.name'"
            :rules="[{required: true, message: '按钮文字不能为空'},{max: 10, message: '最大输入10字'}]">
            <el-input v-model.trim="item.name"></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="9">
          <el-form-item class="style-box"
                        label="样式"
                        :prop="'list.' + index + '.style'"
                        :rules="{required: true, message: '请选择按钮样式'}">
            <el-radio-group v-model="item.style" size="medium">
              <el-radio :label="0">
                <div class="style-normal b1 el-icon-success">文本</div>
              </el-radio>
              <el-radio :label="1">
                <div class="style-normal b2 el-icon-success">文本</div>
              </el-radio>
              <el-radio :label="2">
                <div class="style-normal b3 el-icon-success">文本</div>
              </el-radio>
              <el-radio :label="3">
                <div class="style-normal b4 el-icon-success">文本</div>
              </el-radio>
            </el-radio-group>
          </el-form-item>
        </el-col>
        <el-col :span="8">
          <el-form-item
            label="链接地址"
            :prop="'list.' + index + '.url'"
            :rules="{required: true, message: '链接地址不能为空'}">
            <el-input v-model.trim="item.url"></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="1" class="btn-box">
          <el-button @click="deleteItem(index)" type="primary" icon="el-icon-minus" size="mini" circle></el-button>
        </el-col>
      </el-row>
      <!--<el-form-item>-->
      <!--<el-button type="primary" @click="submitForm('dynamicValidateForm')">提交</el-button>-->
      <!--<el-button @click="addDomain">新增域名</el-button>-->
      <!--<el-button @click="resetForm('dynamicValidateForm')">重置</el-button>-->
      <!--</el-form-item>-->
    </el-form>
    <div @click="addItem" class="add-btn"><i class="el-icon-plus"></i>新建按钮</div>
  </div>
</template>
<script>
  import emitter from 'element-ui/src/mixins/emitter';

  export default {
    name: 'ElDjBtnLinkGroup',
    props: {
      value: {
        type: Array, default() {
          return [];
        }
      },
      max: {type: Number, default: 5}
    },
    mixins: [emitter],
    data() {
      return {
        // btnArr: this.value,
        dynamicValidateForm: {
          list: this.value
        }
      };
    },
    watch: {
      // 用watch监听数组变化，出发父组件值变化
      btnArr() {
        this.dynamicValidateForm.list = this.btnArr;
        this.$emit('input', this.btnArr);
        this.dispatch('ElFormItem', 'el.form.change', [this.btnArr]);
      }
    },
    computed: {
      btnArr() {
        return this.value;
      }
    },
    methods: {
      // 添加
      addItem() {
        if (this.btnArr.length <= this.max - 1) {
          this.btnArr.push({style: 0});
        } else {
          this.$message({
            message: `最多添加${this.max}条`,
            type: 'warning'
          });
        }
      },
      // 删除
      deleteItem(index) {
        this.btnArr.splice(index, 1);
      },
      // 提供给父组件使用的校验函数
      validate(cb) {
        if (this.$refs.dynamicValidateForm) {
          this.$refs.dynamicValidateForm.validate(valid => {
            cb(valid);
          });
        }
      },
      // 提供给父组件使用的重置函数
      resetFields() {
        if (this.$refs.dynamicValidateForm) {
          this.$refs.dynamicValidateForm.resetFields();
        }
      },
      // 提供给父组件使用的重置校验函数
      clearValidate() {
        if (this.$refs.dynamicValidateForm) {
          this.$refs.dynamicValidateForm.clearValidate();
        }
      }
    }
  };
</script>
<style lang="scss">
  /*为了重写element样式，去掉style标签的私有作用域，用class类型来分离作用域*/
  ._dj_btn_link_group {
    background-color: #545C64;
    line-height: 40px;
    ._form {
      padding: 16px 16px 0 16px;
    }
    .el-button.is-circle {
      padding: 6px;
    }
    .el-form-item__label {
      color: white;
    }
    .el-form-item{
      margin-bottom: 0
    }
    .row {
      margin-bottom: 24px;
    }

    .style-box {
      > .el-form-item__label {
        width: 70px !important;
      }
      .el-form-item__content {
        margin-left: 70px !important;
      }
      .el-radio__input {
        display: none;
      }
      .el-radio + .el-radio {
        margin-left: 0;
      }
      .style-normal {
        position: relative;
        display: inline-block;
        padding: 0 8px;
        height: 32px;
        line-height: 32px;
        text-align: center;
        border-radius: 4px;
      }
      .b1 {
        background-color: #FA5967;
        color: white;
        border: 1px solid #FA5967;
      }
      .b2 {
        color: #FFFFFF;
        border: 1px solid #FFFFFF;
      }
      .b3 {
        background: rgba(#FFFFFF, 0.3);
        color: #FFFFFF;
        border: 1px solid rgba(#FFFFFF, 0.3);
      }
      .b4 {
        color: #FA5967;
        border: 1px solid #FA5967;
      }
      label .el-icon-success:before {
        visibility: hidden;
        position: absolute;
        top: 16px;
        right: -6px;
        color: #67C23A;
      }
      label.is-checked .el-icon-success:before {
        visibility: visible;
      }
    }
    .btn-box {
      text-align: right;
    }

    .add-btn {
      line-height: 40px;
      height: 40px;
      color: white;
      text-align: center;
      border-top: solid 1px white;
      cursor: pointer;
    }
  }

</style>


