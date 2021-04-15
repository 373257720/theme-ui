<template>
  <div class="GZ-select">
    <el-select
      :popper-append-to-body="false"
      v-model="value"
      placeholder="Select"
    >
      <el-option
        v-for="item in options"
        :key="item.value"
        :label="item.label"
        :value="item.value"
      >
      </el-option>
    </el-select>
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
    'region': function (newVal, oldVal) {
      this.value = newVal
    },
    value: function (newVal, oldVal) {
      this.$emit('update:region', newVal)
    }
  },
  methods: {}
}
</script>
<style lang='scss'>
.GZ-select {
  .el-icon-arrow-up:before {
    font-family: "iconfont";
    content: "\e61a";
  }
  .el-select .el-input__inner {
    @include border($px: 2px, $shape: solid, $color: #dcdfe6);
    &:focus {
      border-color: $themeColor;
    }
  }
  .el-select-dropdown__item.selected {
    color: $themeColor;
  }
}
</style>
