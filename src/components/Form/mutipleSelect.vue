<template>
  <div class="GZ-mutipleSelect">
    <el-select
      :popper-append-to-body="false"
      v-model="value"
      multiple
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
    regions: Array,
    options: Array
  },
  data () {
    return {
      value: []
    }
  },
  watch: {
    regions: function (newVal, oldVal) {
      this.value = newVal
    },
    value: function (newVal, oldVal) {
      this.$emit('update:regions', newVal)
    }
  },
  methods: {}
}
</script>
<style lang='scss'>
.GZ-mutipleSelect {
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
  .el-select .el-input.is-focus .el-input__inner {
    border-color: $themeColor;
  }
  .el-select-dropdown.is-multiple .el-select-dropdown__item.selected {
    color: $themeColor;
  }
  .el-tag.el-tag--info {
    background-color: #f4f4f5;
    border-color: $themeColor;
    color: $themeColor;
    .el-select .el-tag__close.el-icon-close {
      background-color: none;
      right: -7px;
      top: 0;
      &:before {
        font-family: "iconfont";
        content: "\e68a";
      }
    }
  }
  .el-select .el-tag__close.el-icon-close {
    background-color: none;
    &:hover {
      background-color: none;
    }
  }
}
</style>
