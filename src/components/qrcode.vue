<script setup lang='ts'>
  import { ref } from 'vue'
  import type { Ref } from 'vue'


  defineProps<{
    qrcodeContent: {
      type: String,
      required: true,
      default: ''
    }
  }>()

  
</script>
<template>
  <div>{{ qrcodeContent }}</div>
</template>
<style lang="less" scoped>
</style>
