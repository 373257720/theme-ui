<template>
  <div class="GZ-MessageBox">
    <el-dialog
      title="提示"
      :visible.sync="dialogvisible"
      width="400px"
      :show-close="false"
      :modal="true"
      :close-on-click-modal="false"
      center
    >
      <span>这是一段信息</span>
      <span slot="footer" class="dialog-footer">
        <GZ-button class="firstBtn" @childclick="dialogVisible(false)"
          ><span>取 消</span></GZ-button
        >
        <GZ-button @childclick="dialogVisible(true)"
          ><span>确 定</span></GZ-button
        >
      </span>
    </el-dialog>
  </div>
</template>
<script>
import GZbutton from '@/components/Form/Button'
export default {
  components: {
    'GZ-button': GZbutton
  },
  props: {
    visible: {
      type: Boolean,
      default: function () {}
    }
  },
  data () {
    return {
      dialogvisible: false
    }
  },
  watch: {
    visible: function (newVal, oldVal) {
      this.dialogvisible = newVal
    }
  },
  methods: {
    dialogVisible (istrue) {
      this.$emit('childclick', istrue)
    }
  }
}
</script>
<style lang='scss'>
.GZ-MessageBox{
    .dialog-footer{
        display: flex;
        justify-content: center;
    }
    .firstBtn{
        margin-right: 20px;
    }
}
</style>
