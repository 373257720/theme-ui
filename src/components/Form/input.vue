<template>
  <div class="GZ-input">
    <el-input
      :placeholder="placeholder"
      :clearable="isclearable"
      :show-password="showpassword"
      :style="CombineStyle"
      v-model="curName"
      :disabled="disabled"
    ></el-input>
  </div>
</template>
<script>
export default {
  props: {
    name: String,
    isclearable: {
      type: Boolean,
      default: false
    },
    disabled: {
      type: Boolean,
      default: false
    },
    placeholder: {
      type: String,
      default: 'Please input'
    },
    showpassword: {
      type: Boolean,
      default: false
    },
    styleParameters: Object
  },
  data () {
    return {
      curName: this.name,
      styleData: {
        '--color': '#606266',
        '--width': '60px',
        '--height': '40px',
        '--lineHeight': '40px',
        '--border': '2px',
        '--shape': 'solid',
        '--radius': '0',
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
    name: function (newVal, oldVal) {
      this.curName = newVal
    },
    curName: function (newVal, oldVal) {
      this.$emit('update:name', newVal)
    }
  },
  methods: {}
}
</script>
<style lang='scss' scoped>
.GZ-input {
  /deep/ .el-input {
    .el-input__inner {
      @include Font(
        $FontSize: inherit,
        $lineHeight: var(--lineHeight),
        $color: var(--color)
      );
      @include border(
        $px: var(--border),
        $shape: var(--shape),
        $radius: var(--radius)
      );
      @include boxModel(
        $width: var(--width),
        $height: var(--height),
        $background-color: var(--background),
        $padding: var(--padding)
      );
      &:focus {
        outline: none;
        border-color: $themeColor;
      }
    }
  }
}
</style>
