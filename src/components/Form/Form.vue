<template>
  <div class="GZ-form">
    <el-form
      :model="ruleForm"
      :rules="rules"
      ref="ruleForm"
      label-width="120px"
      class="demo-ruleForm"
    >
      <el-form-item label="活动名称" prop="name">
        <GZ-Input :name.sync="ruleForm.name"></GZ-Input>
      </el-form-item>
      <el-form-item label="活动区域" prop="region">
        <GZ-select
          :region.sync="ruleForm.region"
          :options="options"
        ></GZ-select>
      </el-form-item>
      <el-form-item label="活动区域多选" prop="regions">
        <GZ-mutipleSelect
          :regions.sync="ruleForm.regions"
          :options="options"
        ></GZ-mutipleSelect>
      </el-form-item>
      <el-form-item label="即时配送" prop="delivery">
        <GZ-switch :delivery.sync="ruleForm.delivery"></GZ-switch>
      </el-form-item>
      <el-form-item label="活动性质" prop="type">
        <GZ-checkbox
          :type.sync="ruleForm.type"
          :checkboxList="checkboxList"
        ></GZ-checkbox>
      </el-form-item>
      <el-form-item label="特殊资源" prop="resource">
        <GZ-radio
          :resource.sync="ruleForm.resource"
          :resourceList="options"
        ></GZ-radio>
      </el-form-item>
      <el-form-item label="上传图片">
        <div class="background_picture">
          <el-upload
            action
            list-type="picture-card"
            :limit="1"
            :http-request="
              function (params) {
                return uploadFile(
                  params,
                  'background_picture',
                  'background_picture_id'
                );
              }
            "
            :on-preview="handlePictureCardPreview"
            :file-list="fileList"
            :on-remove="
              function (params) {
                return appear3(params, 'background_picture');
              }
            "
            :on-error="
              function (params) {
                return appear3(params, 'background_picture');
              }
            "
            :before-upload="
              function (params) {
                return dispear3(params, 'background_picture');
              }
            "

          >
            <i class="el-icon-plus"></i>
          </el-upload>
        </div>
      </el-form-item>
      <el-form-item>
        <div class="submit">
          <GZ-button @childclick="submitForm('ruleForm')"
            ><span>提交</span></GZ-button
          >
          <GZ-button @childclick="resetForm('ruleForm')"
            ><span>重置</span></GZ-button
          >
        </div>
      </el-form-item>
    </el-form>
    <GZ-MessageBox
      @childclick="dialogVisible"
      :visible.sync="visible"
    ></GZ-MessageBox>
  </div>
</template>

<script>
import GZInput from '@/components/Form/input'
import GZTextarea from '@/components/Form/textarea'
import GZradio from '@/components/Form/radio'
import GZcheckbox from '@/components/Form/checkbox'
import GZselect from '@/components/Form/select'
import GZmutipleSelect from '@/components/Form/mutipleSelect'
import GZswitch from '@/components/Form/switch'
import GZbutton from '@/components/Form/Button'
import GZMessageBox from '@/components/Notice/MessageBox'
export default {
  components: {
    'GZ-Input': GZInput,
    'GZ-Textarea': GZTextarea,
    'GZ-radio': GZradio,
    'GZ-checkbox': GZcheckbox,
    'GZ-select': GZselect,
    'GZ-mutipleSelect': GZmutipleSelect,
    'GZ-switch': GZswitch,
    'GZ-button': GZbutton,
    'GZ-MessageBox': GZMessageBox
  },
  data () {
    return {
      fileList: [],
      visible: false,
      checkboxList: ['selected and disabled', 'Option A'],
      options: [
        {
          value: 'Option1',
          label: 'Option1'
        },
        {
          value: 'Option2',
          label: 'Option2'
        },
        {
          value: 'Option3',
          label: 'Option3'
        },
        {
          value: 'Option4',
          label: 'Option4'
        },
        {
          value: 'Option5',
          label: 'Option5'
        }
      ],
      ruleForm: {
        name: '',
        region: '',
        date1: '',
        date2: '',
        regions: [],
        delivery: false,
        type: [],
        resource: '',
        desc: ''
      },
      rules: {
        name: [
          { required: true, message: '请输入活动名称', trigger: 'blur' },
          { min: 3, max: 5, message: '长度在 3 到 5 个字符', trigger: 'blur' }
        ],
        region: [
          { required: true, message: '请选择活动区域', trigger: 'change' }
        ],
        regions: [
          { required: true, message: '请选择活动区域', trigger: 'change' }
        ],
        date1: [
          {
            type: 'date',
            required: true,
            message: '请选择日期',
            trigger: 'change'
          }
        ],
        date2: [
          {
            type: 'date',
            required: true,
            message: '请选择时间',
            trigger: 'change'
          }
        ],
        type: [
          {
            type: 'array',
            required: true,
            message: '请至少选择一个活动性质',
            trigger: 'change'
          }
        ],
        resource: [
          { required: true, message: '请选择活动资源', trigger: 'change' }
        ],
        desc: [{ required: true, message: '请填写活动形式', trigger: 'blur' }]
      }
    }
  },
  methods: {

    dialogVisible (isture) {
      this.visible = false
    },
    submitForm (formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          this.visible = true
        } else {
          return false
        }
      })
    },
    resetForm (formName) {
      this.$refs[formName].resetFields()
    }
  }
}
</script>

<style lang="scss">
.GZ-form {
  .el-form-item.is-error .el-input__inner {
    border-color: #f56c6c;
  }
  .GZ-input {
    width: 200px;
  }
  .GZ-select {
    width: 200px;
  }
  .GZ-mutipleSelect {
    width: 200px;
  }
  .submit {
    display: flex;
  }
}
</style>
