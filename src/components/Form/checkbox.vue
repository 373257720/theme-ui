<template>
  <div class="GZ-checkbox">
    <el-checkbox-group v-model="value">
      <el-checkbox
        v-for="item in checkboxList"
        :key="item"
        :label="item"
      ></el-checkbox>
    </el-checkbox-group>
  </div>
</template>
<script>
export default {
  props: {
    type: Array,
    checkboxList: Array
  },
  data () {
    return {
      value: []
    }
  },
  watch: {
    type: function (newVal, oldVal) {
      this.value = newVal
      console.log(this.value)
    },
    value: function (newVal, oldVal) {
      this.$emit('update:type', newVal)
    }
  },
  methods: {
    updateValue (value) {
      //   this.result
    }
  }
}
</script>

<style lang='scss'>
.GZ-checkbox {
  .el-checkbox-group {
    .el-checkbox {
      .el-checkbox__input.is-checked {
        .el-checkbox__inner {
          background-color: $themeColor;
          border-color: $themeColor;
        }
        + .el-checkbox__label {
          color: $themeColor;
        }
      }
      .el-checkbox__inner {
        border-color: #dcdfe6;
        &:after {
          content: "";
          @include prefix(
            $property: transform,
            $value: rotate(45deg) scaleY(1),
            $prefixes: webkit ms moz
          );
          @include boxModel(
            $width: 3px,
            $height: 7px,
            $background-color: none,
            $padding: initial,
            $margin: initial,
            $box-sizing: "content-box"
          );
          @include border($px: 2px, $shape: solid, $color: #fff);
          @include positonAbsolute(
            $vertical: "t",
            $ver: 1px,
            $horizontal: "l",
            $hor: 4px
          );
          border-left: 0;
          border-top: 0;
        }
        &:hover {
          border-color: $themeColor;
        }
      }
    }
  }
}
</style>
