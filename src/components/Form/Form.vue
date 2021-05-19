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
        <GZ-Input
          :styleParameters="{
            '--color': '#606266',
            '--width': '500px',
          }"
          :name.sync="ruleForm.name"
        ></GZ-Input>
      </el-form-item>
      <el-form-item label="活动区域" prop="region">
        <GZ-select
          :styleParameters="{
            '--width': '200px',
          }"
          :region.sync="ruleForm.region"
          :options="options"
        ></GZ-select>
      </el-form-item>
      <el-form-item label="远程搜索">
        <el-select
          v-model="value"
          multiple
          filterable
          remote
          loading-text=""
          element-loading-spinner = "el-icon-loading"  
          placeholder="请输入关键词"
          :remote-method="remoteMethod"
          :loading="loading"
        >
          <el-option
            v-for="item in options"
            :key="item.value"
            :label="item.label"
            :value="item.value"
          >
          </el-option>
        </el-select>
      </el-form-item>
      <el-form-item label="活动区域多选" prop="regions">
        <GZ-mutipleSelect
          :styleParameters="{
            '--color': '#606266',
            '--height': '40px',
            '--width': '500px',
          }"
          :regions.sync="ruleForm.regions"
          :options="options"
        ></GZ-mutipleSelect>
      </el-form-item>
      <el-form-item label="即时配送" prop="delivery">
        <GZ-switch
          :styleParameters="{
            '--width': '200px',
          }"
          :delivery.sync="ruleForm.delivery"
        ></GZ-switch>
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
              (params) => {
                uploadFile(
                  params,
                  'background_picture',
                  'background_picture_id'
                );
              }
            "
            :file-list="fileList"
            :on-remove="
              (params) => {
                appear(params, 'background_picture');
              }
            "
            :on-preview="handlePictureCardPreview"
            :on-error="
              (params) => {
                appear(params, 'background_picture');
              }
            "
            :before-upload="
              (params) => {
                dispear(params, 'background_picture');
              }
            "
          >
            <!-- <div slot="tip"> -->
            <!-- <img src="../../assets/logo.png" alt="" /> -->
            <i class="el-icon-plus"></i>
            <!-- </div> -->
          </el-upload>
          <el-dialog :visible.sync="UploaddialogVisible">
            <img width="100%" :src="dialogImageUrl" alt="" />
          </el-dialog>
        </div>
      </el-form-item>
      <el-form-item label="上传图片">
        <el-upload
          class="upload-demo"
          drag
          action="https://jsonplaceholder.typicode.com/posts/"
          multiple
        >
          <i class="el-icon-upload"></i>
          <div class="el-upload__text">将文件拖到此处，或<em>点击上传</em></div>
          <div class="el-upload__tip" slot="tip">
            只能上传jpg/png文件，且不超过500kb
          </div>
        </el-upload>
      </el-form-item>
      <el-form-item>
        <div class="submit">
          <GZ-button
            :styleParameters="{
              '--width': '100px',
            }"
            @childclick="submitForm('ruleForm')"
            ><span>提交</span></GZ-button
          >
          <GZ-button
            :styleParameters="{
              '--width': '100px',
            }"
            @childclick="resetForm('ruleForm')"
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
      dialogImageUrl: '',
      UploaddialogVisible: false,
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
      },

      options: [],
      value: [],
      list: [],
      loading: false,
      states: [
        'Alabama',
        'Alaska',
        'Arizona',
        'Arkansas',
        'California',
        'Colorado',
        'Connecticut',
        'Delaware',
        'Florida',
        'Georgia',
        'Hawaii',
        'Idaho',
        'Illinois',
        'Indiana',
        'Iowa',
        'Kansas',
        'Kentucky',
        'Louisiana',
        'Maine',
        'Maryland',
        'Massachusetts',
        'Michigan',
        'Minnesota',
        'Mississippi',
        'Missouri',
        'Montana',
        'Nebraska',
        'Nevada',
        'New Hampshire',
        'New Jersey',
        'New Mexico',
        'New York',
        'North Carolina',
        'North Dakota',
        'Ohio',
        'Oklahoma',
        'Oregon',
        'Pennsylvania',
        'Rhode Island',
        'South Carolina',
        'South Dakota',
        'Tennessee',
        'Texas',
        'Utah',
        'Vermont',
        'Virginia',
        'Washington',
        'West Virginia',
        'Wisconsin',
        'Wyoming'
      ]
    }
  },
  mounted () {
    this.list = this.states.map((item) => {
      return { value: `value:${item}`, label: `label:${item}` }
    })
  },
  methods: {
    remoteMethod (query) {
      if (query !== '') {
        this.loading = true
        setTimeout(() => {
          this.loading = false
          this.options = this.list.filter((item) => {
            return item.label.toLowerCase().indexOf(query.toLowerCase()) > -1
          })
        }, 1000)
      } else {
        this.options = []
      }
    },
    styleFunction (
      color,
      width,
      height,
      lineHeight,
      border,
      shape,
      radius,
      background,
      padding
    ) {
      return {
        '--color': '#606266',
        '--width': '100%',
        '--height': '40px',
        '--lineHeight': '40px',
        '--border': '2px',
        '--shape': 'solid',
        '--radius': '5px',
        '--background': 'white',
        '--padding': '0 30px 0 15px'
      }
    },
    handlePictureCardPreview (file) {
      this.dialogImageUrl = file.url
      this.dialogVisible = true
    },
    appear (params, picname) {
      this.handleRemove(
        `.${picname} .el-upload--picture-card`,
        `.${picname} .el-upload-list__item`
      )
      this.ruleForm[`${picname}_id`] = ''
    },
    handlePictureCardPreview (file) {
      this.dialogImageUrl = file.url
      this.UploaddialogVisible = true
    },
    dispear (file, picname) {
      let width
      let height
      const isSize = new Promise(function (resolve, reject) {
        if (!/.(jpg|jpeg|png)$/.test(file.type)) {
          return reject('type_error')
        }
        if (picname === 'background_picture') {
          width = 50
          height = 50
        }
        let _URL = window.URL || window.webkitURL
        let img = new Image()
        img.onload = function () {
          let valid = img.width >= width && img.height >= height
          valid ? resolve() : reject()
        }
        img.src = _URL.createObjectURL(file)
      })
        .then(() => {
          this.choose(
            `.${picname} .el-upload--picture-card`,
            `.${picname} .el-upload-list__item`
          )
          return file
        })
        .catch((err) => {
          if (err === 'type_error') {
            // this.$message.error(this.$t('machines.JPEGJPGPNG'))
          }
          return Promise.reject()
        })
      return isSize
    },
    choose (a) {
      var b = document.querySelector(a)
      b.style = 'display:none;'
    },
    handleRemove (a, b) {
      document.querySelector(a).style =
        'position:absolute;bottom:0;display:block;'
      document.querySelector(b).style = 'display:none'
    },
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
    },
    uploadFile (params, picname, picid) {
      const _file = params.file
      console.log(params)
      // const isLt2M = _file.size / 1024 / 1024 < 2;
      this.formData = new FormData()
      this.formData.append('file', _file)
      console.log(this.formData)
      // this.$axios({
      //   method: "post",
      //   url: `http://atm.wearetechman.com/home/common.picture/upload.html`,
      //   data: this.formData,
      //   headers: {
      //     "Content-Type": "multipart/form-data",
      //   },
      // })
      //   .then((res) => {
      //     if (res.data.ret == 0) {
      //       console.log(res.data);
      //       this.ruleForm[picid] = res.data.data.picture_id;
      //     }
      //   })
      //   .catch((err) => {
      //     console.log(err);
      //   });
    }
  }
}
</script>

<style lang="scss" scoped>
.GZ-form {
  /deep/ .el-form-item.is-error .el-input__inner {
    border-color: #ee3f3f;
  }
  // .GZ-input {
  //   width: 200px;
  // }
  .GZ-select {
    width: 200px;
  }
  .GZ-mutipleSelect {
    width: 200px;
  }
  .submit {
    display: flex;
  }
  .el-upload-list__item.is-success .el-upload-list__item-status-label {
    display: none;
  }
  /deep/ .background_picture {
    position: relative;
    height: 200px;
    width: 400px;
    .el-upload--picture-card {
      bottom: 0;
      width: 100%;
      height: 200px;
      border-color: #c0ccda;
      background: white;
      position: absolute;
    }
    .el-icon-plus {
      line-height: 200px;
    }
    .el-upload-list__item {
      margin: 0;
      // transform: none;
      overflow: hidden;
      bottom: 0;
      width: 100%;
      height: 200px;
      position: absolute;
    }
  }
  /deep/ .upload-demo {
    width: 400px;
  }
}
</style>
