<template>
  <div class="GZ-checkbox">
    <el-checkbox-group v-model="checkList">
      <el-checkbox label="Option A"></el-checkbox>
      <el-checkbox label="Option B"></el-checkbox>
      <el-checkbox label="Option C"></el-checkbox>
      <el-checkbox label="disabled"></el-checkbox>
      <el-checkbox label="selected and disabled"></el-checkbox>
    </el-checkbox-group>
  </div>
</template>
<script>
export default {
  data () {
    return {
      checkList: ['selected and disabled', 'Option A']
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
  width: 180px;
  position: relative;
  font-size: 14px;
  margin-bottom: 30px;
}
</style>
