<template>
<el-button>奥利给！</el-button>
<el-button text @click="dialogVisible = true">
  Click to open Dialog
</el-button>

<el-dialog v-model="dialogVisible" title="弹出层" width="70%"  draggable>
  <iframe src="https://cloud.tencent.com/developer/article/1858458?areaSource=103001.5&traceId=BXTCrvFmGhBwqTe5f8Hpx"  id="testFrame" name="myiframe" frameborder="0" width="100%" height="500" ></iframe>
<!--  <template #footer>-->
<!--    <span class="dialog-footer">-->
<!--      <el-button @click="dialogVisible = false">Cancel</el-button>-->
<!--      <el-button type="primary" @click="dialogVisible = false">-->
<!--        Confirm-->
<!--      </el-button>-->
<!--    </span>-->
<!--  </template>-->

</el-dialog>
</template>

<script setup>
import ElementPlus from 'element-plus'
import 'element-plus/dist/index.css'
import test2 from './test2.vue'
import { ref } from 'vue'

const dialogVisible = ref(false)
let test = test2
</script>

<style scoped>

</style>