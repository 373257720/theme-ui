<template>
  <div class="GZ-mutipleSelect">
    <el-select
      :popper-append-to-body="false"
      v-model="value"
      multiple
      placeholder="Select"
      :style="CombineStyle"
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
    options: Array,
    styleParameters: Object
  },
  data () {
    return {
      value: [],
      styleData: {
        '--color': '#606266',
        '--width': '200px',
        '--height': '40px',
        '--border': '2px',
        '--shape': 'solid',
        '--radius': '5px',
        '--background': 'white',
        '--padding': '0 30px 0 15px'
      },
      CombineStyle: {}
    }
  },
  created () {
    this.CombineStyle = {
      ...this.styleData,
      ...this.styleParameters
    }
    console.log(this.CombineStyle)
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
<style lang='scss' scoped>
 .GZ-mutipleSelect {
  .el-icon-arrow-up:before {
    font-family: "iconfont";
    content: "\e61a";
  }
 /deep/ .el-select .el-input__inner {
    @include border(
      $px: var(--border),
      $shape: var(--shape),
      $radius: var(--radius)
    );
    @include Font(
      $FontSize: inherit,
      $lineHeight: var(--lineHeight),
      $color: var(--color)
    );
    @include boxModel(
      $width: var(--width),
      $height: var(--height),
      $background-color: var(--background),
      $padding: var(--padding)
    );
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
    // border-color: $themeColor;
    // color: $themeColor;
    .el-select .el-tag__close.el-icon-close {
      // background-color: none;
      right: -7px;
      top: 0;
      &:before {
        font-family: "iconfont";
        content: "\e68a";
      }
    }
  }
  .el-select .el-tag__close.el-icon-close {
    // background-color: none;
    // &:hover {
    //   background-color: none;
    // }
  }
}
</style>
