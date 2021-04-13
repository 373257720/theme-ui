<template>
  <div class="GZ-radio">
    <label class="GZ-radio-label" @click="test('1')">
      <span class="GZ-radio__input">
        <span class="GZ-radio__inner"></span>
        <input
          type="radio"
          name="sex"
          tabindex="-1"
          class="GZ-radio__original"
          value="1"
        />
      </span>
      <span class="GZ-radio__label">option a</span>
    </label>
    <label class="GZ-radio-label" @click="test('2')">
      <span class="GZ-radio__input">
        <span class="GZ-radio__inner"></span>
        <input type="radio" name="sex" class="GZ-radio__original" value="2" />
      </span>
      <span class="GZ-radio__label">option b</span>
    </label>
  </div>
</template>
<script>
export default {
  data () {
    return {
      result: ''
    }
  },
  methods: {
    test (num) {
      this.result = num
      console.log(this.result)
    }
    // delectFun (event) {
    //   this.content = ''
    // }
  }
}
</script>

<style lang='scss'>
.GZ-radio {
  width: 180px;
  position: relative;
  font-size: 14px;
  margin-bottom: 30px;
}
</style>
