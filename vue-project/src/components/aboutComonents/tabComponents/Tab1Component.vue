            
<script lang="ts" setup>
import { ref, h, watchEffect } from 'vue';
import { UpOutlined, DownOutlined } from '@ant-design/icons-vue';
import CollapseContent from '../collapseComponents/CollapseContent.vue';
import CollapseContentTab2Vue from '../collapseComponents/CollapseContentTab2.vue';
import CollapseContentTab3Vue from '../collapseComponents/CollapseContentTab3.vue';


const activeKeyTab = ref('1');
const activeKeyCollapse = ref<any>(['1', '2', '3']);
const activeKeyCollapse2 = ref<any>(['4', '5', '6']);
const activeKeyCollapse3 = ref<any>(['7', '8', '9']);

watchEffect(() => {
    console.log(activeKeyCollapse.value)
    console.log(activeKeyCollapse2.value)
    console.log(activeKeyCollapse3.value)
})

const handleCloseCollapseAllInTab = () => {
    if (activeKeyTab.value === "1") {
        activeKeyCollapse.value = []
    } else if (activeKeyTab.value === "2") {
        activeKeyCollapse2.value = []
    } else {
        activeKeyCollapse3.value = []
    }
}

const handleOpenCollapseAllInTab = () => {
    if (activeKeyTab.value === "1") {
        activeKeyCollapse.value = ['1', '2', '3']
    } else if (activeKeyTab.value === "2") {
        activeKeyCollapse2.value = ['4', '5', '6']
    } else {
        activeKeyCollapse3.value = ['7', '8', '9']
    }
}

const handleChildCollapse = (childCollapseKey: any) => {
    if (activeKeyTab.value === "1") {
        activeKeyCollapse.value = childCollapseKey
    } else if (activeKeyTab.value === "2") {
        activeKeyCollapse2.value = childCollapseKey
    } else {
        activeKeyCollapse3.value = childCollapseKey
    }

}

</script>

<template>
    <div class="contentDiv">
        <a-tabs v-model:activeKey="activeKeyTab">
            <a-tab-pane key="1" tab="Tab 1">
                <CollapseContent :collapse-key='activeKeyCollapse' @child-collapse-key="handleChildCollapse"/>
            </a-tab-pane>
            <a-tab-pane key="2" tab="Tab 2">
                <CollapseContentTab2Vue :collapse-key='activeKeyCollapse2' @child-collapse-key="handleChildCollapse"/>
            </a-tab-pane>
            <a-tab-pane key="3" tab="Tab 3">
                <CollapseContentTab3Vue :collapse-key='activeKeyCollapse3' @child-collapse-key="handleChildCollapse"/>
            </a-tab-pane>
            <template #rightExtra>
                <!-- Tab 1 -->
                <div v-if="activeKeyTab === '1'">
                    <a-button shape="circle"
                        :disabled="activeKeyTab === '1' && activeKeyCollapse.length < 1"
                        :icon="h(UpOutlined)" @click="() => { handleCloseCollapseAllInTab() }" />
                    <a-button shape="circle"
                        :disabled="activeKeyTab === '1' && activeKeyCollapse.length === 3"
                        :icon="h(DownOutlined)" @click="() => { handleOpenCollapseAllInTab() }" />
                </div>

                <!-- Tab 2 -->
                <div v-if="activeKeyTab === '2'">
                    <a-button shape="circle"
                        :disabled="activeKeyTab === '2' && activeKeyCollapse2.length < 1"
                        :icon="h(UpOutlined)" @click="() => { handleCloseCollapseAllInTab() }" />
                    <a-button shape="circle"
                        :disabled="activeKeyTab === '2' && activeKeyCollapse2.length === 3"
                        :icon="h(DownOutlined)" @click="() => { handleOpenCollapseAllInTab() }" />
                </div>

                <!-- Tab 3 -->
                <div v-if="activeKeyTab === '3'">
                    <a-button shape="circle"
                        :disabled="activeKeyTab === '3' && activeKeyCollapse3.length < 1"
                        :icon="h(UpOutlined)" @click="() => { handleCloseCollapseAllInTab() }" />
                    <a-button shape="circle"
                        :disabled="activeKeyTab === '3' && activeKeyCollapse3.length === 3"
                        :icon="h(DownOutlined)" @click="() => { handleOpenCollapseAllInTab() }" />
                </div>
            </template>
        </a-tabs>
    </div>
</template>

<style scoped>
.contentDiv {
    margin-left: 30px;
}
</style>