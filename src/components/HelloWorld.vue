<script setup lang="ts">
import { ref } from 'vue-demi'

const count = ref(0)
</script>

<template>
  <div>
    <h2 class="title-text">生成二维码使用</h2>
    <el-button type="primary">按 钮</el-button>
  </div>
</template>

<style lang="less" scoped>
.title-text {
  font-size: 40px;
  color: pink;
}
</style>