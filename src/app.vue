<template>
  <el-container width="100%">
    <el-header>
      <el-button @click="toggleDark()">黑暗/阳光</el-button>
    </el-header>
    <el-container>
      <el-aside width="18%">
          <el-menu
            default-active="2"
            class="el-menu-vertical-demo"
            @open="handleOpen"
            @close="handleClose"
          >
            <el-menu-item index="1" @click="addTabone(editableTabsValue)">
              <span>Navigator One</span>
            </el-menu-item>
            <el-menu-item index="2" @click="addTabtwo(editableTabsValue)">
              <span>Navigator Two</span>
            </el-menu-item>
            <el-menu-item index="3" @click="addTabthree(editableTabsValue)">
              <span>Navigator Three</span>
            </el-menu-item>
            <el-menu-item index="4">
              <span>Navigator Four</span>
            </el-menu-item>
          </el-menu>
      </el-aside>
      <el-main>
<!--        <test v-if="fuck === 'true'"></test>-->
<!--        <test2 v-if="fuck === '2'"></test2>-->

        <el-tabs
          v-model="editableTabsValue"
          type="card"
          class="demo-tabs"
          closable
          @tab-remove="removeTab"
        >
          <el-tab-pane
            v-for="item in editableTabs"
            :key="item.name"
            :label="item.title"
            :name="item.name"
          >
            <iframe v-if="item.web === 'T'" :src="item.content"  :id="item.id" name="myiframe" frameborder="0" width="100%" @load="adjustIframe"></iframe>
            <component v-if="item.web === 'F'" :is='item.content' :objId='objId' @fatherEvent="btnclick" @delTab='delTabs'></component>
          </el-tab-pane>
        </el-tabs>
      </el-main>
    </el-container>
  </el-container>
</template>

<script setup lang="ts">
import {ref} from "vue";
import test from './test.vue'
import test2 from './test2.vue'
import test3 from './test3.vue'

// import { ElNotification } from 'element-plus'
import { useDark, useToggle } from '@vueuse/core'

const isDark = useDark()
const toggleDark = useToggle(isDark)

let iframenumber = ref(0)
function autoiframe(id){
  function adjustIframe(id) {
    var ifm = document.getElementById(id);
    ifm.height = document.documentElement.clientHeight - 60 - 100;
  }

  window.setInterval(function logname() {
      adjustIframe(id)
  }, 1);
}
autoiframe("iframe")

let tabIndex = 2
const editableTabsValue = ref('2')
const editableTabs = ref([
  {
    title: 'Tab 1',
    name: '1',
    web:"T",
    content: "https://cloud.tencent.com/developer/ask/sof/1154665",
    id:"iframe"
  },
  {
    title: 'Tab 2',
    name: '2',
    web:"F",
    content: test2,
    id:"iframe"
  },
])

const addTabone = (targetName: string) => {
  const newTabName = `${++tabIndex}`
  editableTabs.value.push({
    title: '新建标签页1',
    name: newTabName,
    content: test,
    web:"F",
    id:"iframe"
  })
  editableTabsValue.value = newTabName
}

const addTabtwo = (targetName: string) => {
  iframenumber.value = iframenumber.value + 1
  const newTabName = `${++tabIndex}`
  editableTabs.value.push({
    title: 'New Tab2',
    name: newTabName,
    content: "https://cloud.tencent.com/developer/ask/sof/1154665",
    web:"T",
    id:"iframe" + iframenumber.value
  })
  editableTabsValue.value = newTabName
  autoiframe("iframe" + iframenumber.value)
}

const addTabthree = (targetName: string) => {
  iframenumber.value = iframenumber.value + 1
  const newTabName = `${++tabIndex}`
  editableTabs.value.push({
    title: 'New Tab three',
    name: newTabName,
    content: "https://code.xueersi.com/",
    web:"T",
    id:"iframe" + iframenumber.value
  })
  editableTabsValue.value = newTabName
  autoiframe("iframe" + iframenumber.value)
}


const removeTab = (targetName: string) => {
  const tabs = editableTabs.value
  let activeName = editableTabsValue.value
  if (activeName === targetName) {
    tabs.forEach((tab, index) => {
      if (tab.name === targetName) {
        const nextTab = tabs[index + 1] || tabs[index - 1]
        if (nextTab) {
          activeName = nextTab.name
        }
      }
    })
  }

  editableTabsValue.value = activeName
  editableTabs.value = tabs.filter((tab) => tab.name !== targetName)
}

// let fuck = ref("f")
//
// function tab(){
//   fuck.value = "true"
// }
//
// function tab2() {
//   fuck.value = '2'
// }
//
// import type { TabsPaneContext } from 'element-plus'
// const activeName = ref('first')
// const handleClick = (tab: TabsPaneContext, event: Event) => {
//   console.log(tab, event)
// }

</script>

<style scoped>
.el-container {
  height: 100%;
}
.el-header{
  text-align: center;
  line-height: 60px;
}
</style>
