<template>
  <div class="GZ-select">
    <el-select
      :popper-append-to-body="false"
      v-model="value"
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
    options: Array,
    region: String,
    styleParameters: Object
  },
  data () {
    return {
      value: '',
      styleData: {
        '--color': '#606266',
        '--width': '60px',
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
  mounted () {},
  watch: {
    region: function (newVal, oldVal) {
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
    @include border(
      $px: var(--border),
      $shape: var(--shape),
      $radius: var(--radius)
    );
    &:focus {
      border-color: $themeColor;
    }
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
  }
  .el-select-dropdown__item.selected {
    color: $themeColor;
  }
}
</style>
