<template>
  <div class="Mo-input" :class="{ 'Mo-input_suffix': showIcon }">
    <!--    :type="showPassword ? (passwordVisible ? 'text' : 'password') : type" -->
    <input
      class="Mo-input_inner"
      :class="{ 'is-disabled': disabled }"
      :type="inputType"
      :placeholder="placeholder"
      :name="name"
      :disabled="disabled"
      :value="value"
      @input="$emit('input', $event.target.value)"
    />
    <span class="Mo-input_suffix">
      <!-- v-if="clearable && value"  传了clearable 并且value 存在 在显示-->
      <i
        class="Mo-icon-guanbi"
        v-if="clearable && value && type !== 'password'"
        @click="clear"
      ></i>
      <i
        class="Mo-icon-yanjing"
        :class="{ 'password-icon-active': passwordVisible }"
        v-if="showPassword && type == 'password'"
        @click="handlePassword"
      ></i>
    </span>
  </div>
</template>

<script>
export default {
  name: "MoInput",
  data() {
    // 控制是否显示密码框
    return {
      passwordVisible: false,
    };
  },
  props: {
    placeholder: {
      type: String,
      default: "",
    },
    type: {
      type: String,
      default: "text",
    },
    name: {
      type: String,
      default: "",
    },
    disabled: {
      type: Boolean,
      default: false,
    },
    value: {
      type: String,
      default: "",
    },
    clearable: {
      type: Boolean,
      default: false,
    },
    showPassword: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    clear() {
      this.$emit("input", "");
    },
    handlePassword() {
      this.passwordVisible = !this.passwordVisible;
    },
  },
  computed: {
    showIcon() {
      return this.clearable || this.showPassword;
    },
    inputType() {
      return this.showPassword
        ? this.passwordVisible
          ? "text"
          : "password"
        : this.type;
    },
  },
};
</script>

<style lang="scss">
.Mo-input {
  display: inline-block;
  width: 100%;
  position: relative;
  font-size: 14px;
  .Mo-input_inner {
    -webkit-appearance: none;
    background-color: #fff;
    background-image: none;
    border: 1px solid #dcdfe6;
    border-radius: 4px;
    box-sizing: border-box;
    color: #606266;
    display: inline-block;
    font-size: inherit;
    height: 40px;
    line-height: 40px;
    outline: none;
    padding: 0 15px;
    transition: border-color 0.2s cubic-bezier(0.645, 045, 0.355, 1);
    width: 100%;

    &:focus {
      outline: none;
      border-color: #409eff;
    }
    // input禁用样式
    &.is-disabled {
      background-color: #f5f7fa;
      border-color: #e4e7ed;
      color: #c0c4cc;
      cursor: not-allowed;
    }
  }
}

.Mo-input_suffix {
  .Mo-input_inner {
    padding-right: 30px;
  }
  .Mo-input_suffix {
    position: absolute;
    right: 10px;
    height: 100%;
    top: 0;
    line-height: 40px;
    text-align: center;
    color: #c0c4cc;
    transition: all 0.3s;
    z-index: 900;
    i {
      color: #c0c4cc;
      font-size: 14px;
      cursor: pointer;
      transition: color 0.2s cubic-bezier(0.645, 0.045, 0.355, 1);
      &.password-icon-active {
        color: blue;
      }
    }
  }
}
</style>
