<template>
  <div class="GZ-radio">
    <el-radio-group v-model="radio">
      <el-radio
        v-for="item in resourceList"
        :key="item.value"
        :label="item.label"
        >{{ item.label }}</el-radio
      >
    </el-radio-group>
  </div>
</template>
<script>
export default {
  props: {
    resource: {
      type: String,
      default: function () {}
    },
    resourceList: {
      type: Array,
      default () {
        return []
      }
    }
  },
  data () {
    return {
      radio: ''
    }
  },
  watch: {
    resource: function (newVal, oldVal) {
      this.radio = newVal
    },
    radio: function (newVal, oldVal) {
      this.$emit('update:resource', newVal)
    }
  },
  methods: {}
}
</script>
<style lang='scss'>
.GZ-radio {
  .el-radio-group {
    .el-radio__inner {
      @include border($px: 1px, $shape: solid, $color: #dcdfe6, $radius: 2px);
      &:hover {
        border-color: $themeColor;
      }
    }
    .el-radio__input.is-checked {
      .el-radio__inner {
        border-color: $themeColor;
        background: $themeColor;
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
      }
      + .el-radio__label {
        color: $themeColor;
      }
    }
  }
}
</style>
