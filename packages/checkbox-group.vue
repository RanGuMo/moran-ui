<template>
  <div class="Mo-checkbox-group">
    <slot></slot>
  </div>
</template>
<script>
export default {
  name: 'MoCheckboxGroup',
  provide () {
    return {
      CheckboxGroup: this
    }
  },
  props: {
    value: {
      type: Array
    }
  }
}
</script>
