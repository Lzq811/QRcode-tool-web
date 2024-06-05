<script setup lang='ts'>
  import { ref } from 'vue-demi'
  import type { Ref } from 'vue-demi'
  import edit from './edit.vue'
  import qrcode from './qrcode.vue'


  const qrcodeContent:Ref<string> = ref('')

  const generateQRcontent = (val:string) => {
    qrcodeContent.value = val
    console.log('generateQRcontent', qrcodeContent.value)
  }

</script>
<template>
  <el-row class="container" justify="space-evenly">
    <el-col class="col-item" :span="15">
      <edit @generateQRcontent="generateQRcontent" />
    </el-col>
    <el-col class="col-item" :span="8">
      <qrcode :qrcodeContent="qrcodeContent" />
    </el-col>
  </el-row>
</template>
<style lang="less" scoped>
.container {
  width: 100%;
  height: 100%;
  .col-item {
    border: 1px solid red;
  }
}
</style>
