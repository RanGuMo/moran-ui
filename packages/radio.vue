<template>
  <label class="Mo-radio" :class="{ 'is-checked': label === model }">
    <span class="Mo-radio_input">
      <span class="Mo-radio_inner"></span>
      <input
        type="radio"
        class="Mo-radio_original"
        :name="name"
        :value="label"
        v-model="model"
      />
    </span>
    <span class="Mo-radio_label">
      <slot></slot>
      <!-- 如果没有传值，就把label作为文本显示 -->
      <template v-if="!$slots.default">{{ label }}</template>
    </span>
  </label>
</template>
<script>
export default {
  name: "MoRadio",
  props: {
    value: null,
    name: {
      type: String,
      default: "",
    },
    label: {
      type: [String, Number, Boolean],
      default: "",
    },
  },
  inject: {
    RadioGroup: {
      default: "",
    },
  },
  computed: {
    model: {
      get() {
        // return this.value;
        return this.isGroup ? this.RadioGroup.value : this.value;
      },
      set(value) {
        // 通过v-model绑定的值，通过input事件传递给父组件
        // this.$emit("input", value);
        this.isGroup
          ? this.RadioGroup.$emit("input", value)
          : this.$emit("input", value);
      },
    },
    // 判断是否使用了 radio-group 组件
    isGroup() {
      return !!this.RadioGroup;
    },
  },
};
</script>
<style lang="scss" scoped>
.Mo-radio {
  color: #606266;
  font-weight: 500;
  line-height: 1;
  position: relative;
  cursor: pointer;
  display: inline-block;
  white-space: nowrap;
  outline: none;
  font-size: 14px;
  margin-right: 30px;
  -moz-user-select: none;
  -webkit-user-select: none;
  -moz-user-select: none;
  .Mo-radio_input {
    white-space: nowrap;
    cursor: pointer;
    outline: none;
    display: inline-block;
    line-height: 1;
    position: relative;
    vertical-align: middle;
    .Mo-radio_inner {
      border: 1px solid #dcdfe6;
      border-radius: 100%;
      width: 14px;
      height: 14px;
      background-color: #fff;
      position: relative;
      cursor: pointer;
      display: inline-block;
      box-sizing: border-box;
      &:after {
        width: 4px;
        height: 4px;
        border-radius: 100%;
        background-color: #fff;
        content: "";
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%) scale(0);
        transition: transform 0.15s ease-in;
      }
    }
    .Mo-radio_original {
      opacity: 0;
      outline: none;
      position: absolute;
      z-index: -1;
      top: 0;
      left: 0px;
      right: 0;
      bottom: 0;
      margin: 0;
    }
  }
  .Mo-radio_label {
    font-size: 14px;
    padding-left: 10px;
  }
}
// 选中的样式
.Mo-radio.is-checked {
  .Mo-radio_input {
    .Mo-radio_inner {
      border-color: #409eff;
      background-color: #409eff;
      &:after {
        transform: translate(-50%, -50%) scale(1);
      }
    }
  }
  .Mo-radio_label {
    color: #409eff;
  }
}
</style>
