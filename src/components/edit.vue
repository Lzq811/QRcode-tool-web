<script setup lang='ts'>
import { ref, reactive, defineEmits } from 'vue'
import type { Ref } from 'vue'
import type { TabsPaneContext, ComponentSize, FormInstance, FormRules } from 'element-plus'
import { ElMessage } from 'element-plus'

interface IterTabItem {
  id: string
  name: number | string
  label: string
}
interface IterForm {
  netUrl: string
}

const emit = defineEmits(['generateQRcontent'])

const TabList:Ref<Array<IterTabItem>> = ref([
  { id: '00001', name: '0', label: '网址' },
  { id: '00002', name: '1', label: '文本' },
  { id: '00003', name: '2', label: '表单' }
])
const activeName:Ref<string | undefined> = ref('0')
const currentContent:Ref<string> = ref('')

const ruleFormRef = ref<FormInstance>()
const ruleForm = reactive<IterForm>({
  netUrl: 'https://www.baidu.com'
})

const handleClick = (tab: TabsPaneContext) => {
  // console.log('index', typeof tab.index) // string
  activeName.value = tab.index
}

const submitForm = async () => {
  switch (activeName.value) {
    case '0':
      netAddress()
      break
    default:
      netAddress()
      break
  }
}
const resetForm = (formEl: FormInstance | undefined) => {
  if (!formEl) return
  formEl.resetFields()
}

const netAddress = () => {
  if (ruleForm.netUrl && ruleForm.netUrl.length > 0) {
    currentContent.value = ruleForm.netUrl
    generateQRcode()
  } else {
    ElMessage.error('请输入正确的网络地址信息!')
  }
}

const generateQRcode = () => {
  // console.log(currentContent.value)
  emit('generateQRcontent', currentContent.value)
}

</script>
<template>
  <div class="edit-container">
    <el-tabs v-model="activeName" class="demo-tabs" @tab-click="handleClick">
      <el-tab-pane v-for="tab in TabList" :label="tab.label" :name="tab.name" :key="tab.id"></el-tab-pane>
    </el-tabs>
    <el-form
      ref="ruleFormRef"
      label-position="right"
      label-width="auto"
      :model="ruleForm"
    >
      <el-form-item label="网络地址" v-if="activeName === '0'">
        <el-input v-model="ruleForm.netUrl" placeholder="请输入网络地址" prop="netUrl" />
      </el-form-item>
      <!-- <el-form-item label="Activity zone">
        <el-input v-model="formLabelAlign.region" />
      </el-form-item>
      <el-form-item label="Activity form">
        <el-input v-model="formLabelAlign.type" />
      </el-form-item> -->
      <el-form-item style="float: right;">
        <el-button type="primary" @click="submitForm(ruleFormRef)">生成二维码</el-button>
        <el-button @click="resetForm(ruleFormRef)">重置</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>
<style lang="less" scoped>

</style>
