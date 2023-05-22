<template>
  <div class="Mo-switch" @click="handlerClick" :class="{ 'is-checked': value }" >
    <span class="Mo-switch_core" ref="core">
      <span class="Mo-switch_button"></span>
    </span>
    <!-- 用户在使用switch组件的时候，实质上是当成表单元素来使用的。
      因此可能会用到组件的name属性。所以需要在switch组件中添加一个checkbox，
      并且当值改变的时候，也需要设置checkbox的value值。 -->
    <input type="checkbox" class="Mo-switch_input" :name="name" ref="input">
  </div>
</template>

<script>
export default {
  name: "MoSwitch",
  props: {
    value: {
      type: Boolean,
      default: false,
    },
    activeColor: {
      type: String,
      default: "",
    },
    inactiveColor: {
      type: String,
      default: "",
    },
    name: {
      type: String,
      default: "",
    }
  },
  methods: {
    handlerClick() {
      this.$emit("input", !this.value);
      // 控制checkbox的值,input值同步value值
     this.$refs.input.checked = this.value
    },
    setColor() {
      // 修改开关颜色，如果传入了activeColor和inactiveColor
      if (this.activeColor || this.inactiveColor) {
        let color = !this.value ? this.inactiveColor : this.activeColor;
        this.$refs.core.style.borderColor = color;
        this.$refs.core.style.backgroundColor = color;
      }
      // 控制checkbox的值,input值同步value值
       this.$refs.input.checked = this.value
    },
  },
  mounted() {
    this.setColor();
  },
  watch: {
    // 监听 value 的变化，如果传入了activeColor和inactiveColor
    // 则修改开关颜色
    value() {
      this.setColor();
    }
  },
};
</script>

<style lang="scss" scoped>
.Mo-switch {
  display: inline-block;
  align-items: center;
  position: relative;
  font-size: 14px;
  line-height: 20px;
  vertical-align: middle;
  .Mo-switch_core {
    margin: 0;
    display: inline-block;
    position: relative;
    width: 40px;
    height: 20px;
    border: 1px solid #dcdfe6;
    outline: none;
    border-radius: 10px;
    box-sizing: border-box;
    background: #dcdfe6;
    cursor: pointer;
    transition: border-color 0.3s, background-color 0.3s;
    vertical-align: middle;
    .Mo-switch_button {
      position: absolute;
      top: 1px;
      left: 1px;
      border-radius: 100%;
      transition: all 0.3s;
      width: 16px;
      height: 16px;
      background-color: #fff;
    }
  }
}

// 选中样式
.is-checked {
  .Mo-switch_core {
    border-color: #409eff;
    background-color: #409eff;
    .Mo-switch_button {
      transform: translateX(20px);
    }
  }
}

  // 隐藏input标签
  .Mo-switch_input{
    position:absolute;
    width: 0;
    height: 0;
    opacity: 0;
    margin: 0;
  }
</style>
