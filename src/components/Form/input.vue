<template>
  <div class="GZ-input">
    <el-input placeholder="Please input" clearable v-model="curName"></el-input>
  </div>
</template>
<script>
export default {
  props: {
    name: String,
  },
  data() {
    return {
      curName: this.name,
    };
  },
  watch: {
    name: function (newVal, oldVal) {
      this.curName = newVal;
    },
    curName: function (newVal, oldVal) {
      this.$emit("update:name", newVal);
    },
  },
  methods: {},
};
</script>

<style lang='scss'>
.GZ-input {
  @include Font($FontSize: inherit, $lineHeight: 40px, $color: #606266);
  .el-input__inner {
    @include border($px: 2px, $shape: solid, $color: #dcdfe6, $radius: 0);
    @include boxModel(
      $width: 100%,
      $height: 40px,
      $background-color: #fff,
      $padding: 0 30px 0 15px
    );
    &:focus {
      outline: none;
      border-color: $themeColor;
    }
  }
}
</style>
