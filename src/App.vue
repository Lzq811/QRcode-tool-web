<script setup lang="ts">
import { ElConfigProvider } from 'element-plus'
import HelloWorld from './components/HelloWorld.vue'

import {ref} from 'vue-demi'

const size:string = ref('default') // 默认大小主体
const zIndex:Number = ref(3000)
</script>

<template>
  <el-config-provider :size="size" :z-index="zIndex">
    <HelloWorld />
  </el-config-provider>
</template>

