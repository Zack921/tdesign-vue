<template>
  <div class="t-upload__file-flow-demo">
    <t-upload
      v-model="files"
      action="https://service-bv448zsw-1257786608.gz.apigw.tencentcs.com/api/upload-demo"
      placeholder="批量合并上传，会通过一个接口上传所有的文件"
      theme="file-flow"
      multiple
      isBatchUpload
      uploadAllFilesInOneRequest
      :auto-upload="false"
      :max="10"
      @success="handleUploadSuccess"
    ></t-upload>
  </div>
</template>

<script>
export default {
  name: 'TUploadFileFlow',

  data() {
    return {
      files: [],
    };
  },

  methods: {
    handleUploadSuccess(e) {
      console.log('batch upload', e);
    },
  },
};
</script>
