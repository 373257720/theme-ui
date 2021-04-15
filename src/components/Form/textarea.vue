/* eslint-disable no-undef */
<template>
  <div class="GZ-textarea">
    <el-input
      type="textarea"
      :autosize="{ minRows: 2, maxRows: 10 }"
      placeholder="Please input"
      v-model="textarea2"
    >
    </el-input>
  </div>
</template>
<script>
export default {
  data () {
    return {
      textarea2: ''
    }
  },
  created () {},
  methods: {}
}
</script>
<style lang='scss'>
.GZ-textarea {
  width: 180px;
  @include Font($FontSize: 14px, $lineHeight: 1.5, $color: #606266);
  margin-bottom: 30px;
  .el-textarea__inner {
    font-family: inherit;
    @include border($px: 2px, $shape: solid, $color: #dcdfe6);
    @include boxModel(
      $width: 100%,
      $height: 54px,
      $background-color: #fff,
      $padding: 5px 15px
    );
    &:focus {
      outline: none;
      border-color: $themeColor;
    }
  }
}
</style>
