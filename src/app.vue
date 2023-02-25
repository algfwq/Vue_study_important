<template>
  <el-container width="100%">
    <el-header>奥利给开发者IDE</el-header>
    <el-container>
      <el-aside width="18%">
          <el-menu
            default-active="2"
            class="el-menu-vertical-demo"
            @open="handleOpen"
            @close="handleClose"
          >
            <el-menu-item index="1" @click="addTab(editableTabsValue)">
              <span>Navigator One</span>
            </el-menu-item>
            <el-menu-item index="2" @click="tab()">
              <span>Navigator Two</span>
            </el-menu-item>
            <el-menu-item index="3" @click="tab2()">
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
            <component :is='item.content' :objId='objId' @fatherEvent="btnclick" @delTab='delTabs'></component>
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

let tabIndex = 2
const editableTabsValue = ref('2')
const editableTabs = ref([
  {
    title: 'Tab 1',
    name: '1',
    content: test,
  },
  {
    title: 'Tab 2',
    name: '2',
    content: test2,
  },
])

const addTab = (targetName: string) => {
  const newTabName = `${++tabIndex}`
  editableTabs.value.push({
    title: 'New Tab',
    name: newTabName,
    content: test3,
  })
  editableTabsValue.value = newTabName
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
.el-header,
.el-footer {
  background-color: #0be5a4;
  color: #333;
  text-align: center;
  line-height: 60px;
}

/*.el-main {*/
/*  background-color: #e9eef3;*/
/*  color: #333;*/
/*  text-align: center;*/
/*  line-height: 160px;*/
/*}*/
</style>
