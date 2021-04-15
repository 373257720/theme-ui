<template>
  <div class="GZ-switch">
    <el-switch
      v-model="value"
      :width="40"
      active-color="#58bc58"
      inactive-color="#dcdfe6"
    >
    </el-switch>
  </div>
</template>
<script>
export default {
  props: {
    delivery: Boolean
  },
  data () {
    return {
      value: ''
    }
  },
  watch: {
    'delivery': function (newVal, oldVal) {
      this.value = newVal
    },
    value: function (newVal, oldVal) {
      this.$emit('update:delivery', newVal)
    }
  },
  methods: {}
}
</script>
<style lang='scss'>
.GZ-switch {
  $el-switch: 20px; //switch 高度
  $el-switch__core_height: 16px; //圆圈高度
  .el-switch {
    height: $el-switch;
    .el-switch__core {
      height: 100%;
      border-radius: $el-switch / 2;
    }
  }
  .el-switch.is-checked .el-switch__core::after {
    margin-left: -$el-switch__core_height - 1px;
  }
  .el-switch__core:after {
    width: $el-switch__core_height;
    height: $el-switch__core_height;
    top: 50%;
    @include prefix($property:transform, $value:translateY(-50%), $prefixes:webkit ms moz);
  }
}
</style>
