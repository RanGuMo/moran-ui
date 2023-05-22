<template>
  <transition name="Mo-dialog-fade">
  <div class="Mo-dialog_wrapper" @click.self="handleClose" v-show="visible">
    <div class="Mo-dialog" :style="{width:width,marginTop:top}">
      <div class="Mo-dialog_header">
        <!-- 用slot套 span 有三种好处，1.如果不传slot为title 的插槽，则默认使用 span
        2.如果不传slot为title 的插槽，但传了title的值，则可以修改title内容
      3，如果 传了title的插槽，就用插槽的内容 -->
        <slot name="title">
          <span class="Mo-dialog_title">{{title}}</span>
        </slot>
        <button class="Mo-dialog_headerbtn" @click="handleClose">
          <i class="Mo-icon-guanbi"></i>
        </button>
      </div>
      <div class="Mo-dialog_body">
        <slot>
          <span>这是一段信息</span>
        </slot>
      </div>
      <div class="Mo-dialog_footer" if="$slots.footer">
        <slot name="footer"></slot>
      </div>
    </div>
  </div>
</transition>
 </template>

<script>
  export default {
  name: 'MoDialog',
  props: {
    title: {
      type: String,
        default:'提示'
    },
    width: {
      type: String,
        default:'50%'
    },
    top: {
      type: String,
        default:'15vh'
    },
    visible: {
      type: Boolean,
        default:false
      }
  },
     methods: {
       handleClose(){
         this.$emit('update:visible',false)
       }
     }
  }
</script>

<style lang="scss" scoped>
.Mo-dialog_wrapper{
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  overflow: auto;
  margin: 0;
  z-index: 2001;
  background-color: rgba(0,0,0,0.5);
  .Mo-dialog{
    position: relative;
    margin: 15vh auto 50px;
    background: #fff;
    border-radius: 2px;
    box-shadow: 0 1px 3px rgba(0,0,0,0.3);
    box-sizing: border-box;
    width: 30%;
    &_header{
      padding: 20px 20px 10px;
      .Mo-dialog_title{
        line-height: 24px;
        font-size: 18px;
        color: #303133;
      }
      .Mo-dialog_headerbtn{
        position: absolute;
        top: 20px;
        right: 20px;
        padding: 0;
        background: transparent;
        border: none;
        outline: none;
        cursor: pointer;
        font-size: 16px;
        .Mo-icon-guanbi{
          color:909399
        }
      }
    }
    &_body{
      padding: 30px 20px;
      color: #606266;
      font-size: 14px;
      word-break: break-all;
    }
    &_footer{
      padding: 10px 20px 20px;
      text-align: right;
      box-sizing: border-box;
      ::v-deep .Mo-button:first-child{
        margin-right: 20px;
      }
    }
  }
}

// 动画过渡
.Mo-dialog-fade-enter-active{
  animation:run .3s;
}
.Mo-dialog-fade-leave-active{
  animation:run .3s reverse;
}

@keyframes run{
  0%{
    opacity: 0;
    transform: translateY(-20px);
  }
  100%{
    opacity: 1;
    transform: translateY(0px);
  }
}


</style>
