<template>
  <div class="GZ-input">
    <input
      class="my-number-input"
      placeholder="please input"
      @focus="
        () => {
          leave = true;
        }
      "
      v-model="content"
    />
    <span
      @click="
        () => {
          content = '';
        }
      "
      class="GZ-input__suffix iconfont"
      :class="{ 'icon-shanchu': content && leave }"
    >
    </span>
  </div>
</template>
<script>
export default {
  data() {
    return {
      content: "",
      leave: true,
    };
  },
  methods: {
    // delectFun (event) {
    //   this.content = ''
    // }
  },
};
</script>

<style lang='scss'>
.GZ-input {
  width: 180px;
  position: relative;
  font-size: 14px;
  margin-bottom: 30px;
  // display: inline-block;
  // vertical-align: bottom;
  .my-number-input {
    z-index: $z-Index88;
    -webkit-appearance: none;
    background-image: none;
    display: inline-block;
    outline: none;
    transition: border-color 0.2s cubic-bezier(0.645, 0.045, 0.355, 1);
    @include Font(inherit, 40px, #606266);
    @include border(1px, solid, #dcdfe6, 4px);
    @include boxModel(100%, 40px, #fff, 0 30px 0 15px);
    &:focus {
      outline: none;
      border-color: $themeColor;
    }
  }
  .GZ-input__suffix {
    z-index: $default-Index;
    color: $themeColor;
    cursor: pointer;
    @include positonAbsolute("m", 0, "r", 10px);
  }
}
</style>
