<template>
  <div class="color_picker_container">
    <span>{{labelData}}</span>
    <div class="color_cell">
      <el-upload
        class="upload-demo"
        ref="upload"
        action="suibianxie"
        :limit="1"
        :on-preview="handlePreview"
        :on-remove="handleRemove"
        :on-change="handleUpLoadChange"
        :file-list="fileList"
        :auto-upload="false"
      >
        <el-button slot="trigger" size="small" type="primary">选取文件</el-button>
        <!-- <el-button
              style="margin-left: 10px;"
              size="small"
              type="success"
              @click="submitUpload"
        >上传到服务器</el-button>-->
        <!-- <div slot="tip" class="el-upload__tip">只能上传jpg/png文件，且不超过500kb</div> -->
      </el-upload>
    </div>
  </div>
</template>

<script>
import fieldMixins from './field_mixins'
export default {
  mixins: [fieldMixins],
  computed: {
    // ...mapState('partComponent', ['activedWidget'])
    fileList() {
      return this.modelData ? [{
        name: '',
        url: this.modelData
      }] : []
    }
  },
  methods: {
    handleUpLoadChange(file, fileList) {
      var event = window.event
      var file2 = event.target.files[0]
      var reader = new FileReader()
      // 转base64
      reader.onload = (e) => {
        const imgUrl = e.target.result
        this.handleFieldModelChange(imgUrl)
        // _this.imageUrl = e.target.result // 将图片路径赋值给src
      }
      reader.readAsDataURL(file2)
    },

    handlePreview(file) {},

    handleRemove(file, fileList) {
      this.handleFieldModelChange('')
    }
  }
}
</script>

<style lang="scss" scoped>
.color_picker_container {
  display: flex;
  width: 100%;
  height: 60px;
  align-items: center;
  .color_cell {
    margin-left: 10px;
  }
}
</style>
