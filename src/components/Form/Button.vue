<template>
  <el-button class="GZ-button" :style="CombineStyle" @click="childclick">
    <slot></slot>
  </el-button>
</template>
<script>
export default {
  props: {
    // options: Array,
    // region: String
    styleParameters: Object
  },
  data () {
    return {
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
      // value: ''
    }
  },
  created () {
    this.CombineStyle = {
      ...this.styleData,
      ...this.styleParameters
    }
    console.log(this.CombineStyle)
  },
  watch: {},
  methods: {
    childclick () {
      this.$emit('childclick')
    }
  }
}
</script>
<style lang='scss'>
.GZ-button.el-button {
  @include boxModel(
    $width: var(--width),
    $height: var(--height),
    $background-color: $themeColor
  );
  @include Font();
  @include border($radius: var(--radius));
  &:hover {
    // color: #fff;
    background-color: #58bc58;
  }
  &:active {
    // color: #93c093ec;
    background-color: $themeColor;
    // border-color: #93c093ec;
    // outline: 0;
  }
}
</style>
