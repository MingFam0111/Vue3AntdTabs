<script setup lang="ts">
import { ref, onMounted, h, watchEffect } from "vue";

import { tabObject } from "./tabObject";
import SubTab1 from "./SubTab/SubTab1.vue";

import { UpOutlined, DownOutlined } from "@ant-design/icons-vue";

const activeKey = ref();
const emitChangeSubTab = ref();
const emitCollapseObject = ref(tabObject[0].subTab[0].collapseObject);
const newTabObject = ref(tabObject);

onMounted(() => {
  activeKey.value = tabObject[0].tabKey;
});

const handleCloseCollapse = () => {
  for (let i = 0; i < newTabObject.value.length; i++) {
    for (let j = 0; j < newTabObject.value[i].subTab.length; j++)
      if (newTabObject.value[i].subTab[j].subTabKey === emitChangeSubTab.value) {
        newTabObject.value[i].subTab[j].collapseObject = [];
        emitCollapseObject.value = newTabObject.value[i].subTab[j].collapseObject;
      }
  }
};

const handleOpenCollapse = () => {
  for (let i = 0; i < newTabObject.value.length; i++) {
    for (let j = 0; j < newTabObject.value[i].subTab.length; j++)
      if (newTabObject.value[i].subTab[j].subTabKey === emitChangeSubTab.value) {
        newTabObject.value[i].subTab[j].collapseObject = ["1", "2", "3"];
        emitCollapseObject.value = newTabObject.value[i].subTab[j].collapseObject;
      }
  }
};

const handleChange = (e: any) => {
  for (let i = 0; i < newTabObject.value.length; i++) {
    if (newTabObject.value[i].tabKey === e) {
      emitChangeSubTab.value = newTabObject.value[i].subTab[0].subTabKey;
      emitCollapseObject.value = newTabObject.value[i].subTab[0].collapseObject;
    }
  }
};

const handleEmitChangeSubTab = (e: any) => {
  emitChangeSubTab.value = e;
  console.log(e, "first")
};

const handleEmitCollapseObject = (e: any) => {
  for (let i = 0; i < newTabObject.value.length; i++) {
    for (let j = 0; j < newTabObject.value[i].subTab.length; j++)
      if (newTabObject.value[i].subTab[j].subTabKey === emitChangeSubTab.value) {
        newTabObject.value[i].subTab[j].collapseObject = e;
        emitCollapseObject.value = newTabObject.value[i].subTab[j].collapseObject;
      }
  }
};
</script>

<template>
  <div class="contentDiv">
    <a-tabs v-model:activeKey="activeKey" center type="card" @change="handleChange">
      <a-tab-pane :key="tabObject[0].tabKey" :tab="tabObject[0].tabName">
        <SubTab1 :subTabObject="tabObject[0].subTab" :newTabObject="newTabObject[0].subTab" :parentActiveKey = "activeKey"
          @activeSubTabKeyOnChange="handleEmitChangeSubTab" @emitCollapseObject="handleEmitCollapseObject" />
      </a-tab-pane>
      <a-tab-pane :key="tabObject[1].tabKey" :tab="tabObject[1].tabName">
        <SubTab1 :subTabObject="tabObject[1].subTab" :newTabObject="newTabObject[1].subTab" :parentActiveKey = "activeKey"
          @activeSubTabKeyOnChange="handleEmitChangeSubTab" @emitCollapseObject="handleEmitCollapseObject" />
      </a-tab-pane>
      <a-tab-pane :key="tabObject[2].tabKey" :tab="tabObject[2].tabName">
        <SubTab1 :subTabObject="tabObject[2].subTab" :newTabObject="newTabObject[2].subTab" :parentActiveKey = "activeKey"
          @activeSubTabKeyOnChange="handleEmitChangeSubTab" @emitCollapseObject="handleEmitCollapseObject" />
      </a-tab-pane>
      <template #rightExtra>
        <div>
          <a-button shape="circle" :disabled="emitCollapseObject.length === 0" :icon="h(UpOutlined)" @click="() => {
            handleCloseCollapse();
          }
            " />
          <a-button shape="circle" :disabled="emitCollapseObject.length === 3" :icon="h(DownOutlined)" @click="() => {
            handleOpenCollapse();
          }
            " />
        </div>
      </template>
    </a-tabs>
  </div>
</template>

<style scoped>
.contentDiv {
  margin: 20px;
}
</style>
