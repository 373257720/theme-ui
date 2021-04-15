<template>
  <div class="GZ-button">
    <el-button @click="childclick">
        <slot></slot>
    </el-button>
  </div>
</template>
<script>
export default {
  props: {
    options: Array,
    region: String
  },
  data () {
    return {
      value: ''
    }
  },
  watch: {
    region: function (newVal, oldVal) {
      this.value = newVal
    },
    value: function (newVal, oldVal) {
      this.$emit('update:region', newVal)
    }
  },
  methods: {
    childclick () {
      this.$emit('childclick')
    }
  }
}
</script>
<style lang='scss'>
.GZ-button {
  .el-button {
    &:focus,
    &:hover {
      color: #fff;
      border-color: $themeColor;
      background-color: $themeColor;
    }
    &:active {
      color: #93c093ec;
      border-color: #93c093ec;
      outline: 0;
    }
  }
}
</style>
