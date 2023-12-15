<script setup lang="ts">
import { ref, onMounted, watch } from 'vue';
import CollapseComponent from './CollapseComponent.vue';

const props = defineProps(['subTabObject', 'newTabObject', 'parentActiveKey'])

const emit = defineEmits(['activeSubTabKeyOnChange', 'emitCollapseObject'])

const activeKey = ref();
const collapseObject = ref()

onMounted(() => {
    activeKey.value = props.subTabObject[0].subTabKey
    emit('activeSubTabKeyOnChange', activeKey.value)
})

watch(() => props.parentActiveKey, () => {
  // Update activeKey when parentActiveKey changes
  activeKey.value = props.subTabObject[0].subTabKey;
  emit('activeSubTabKeyOnChange', activeKey.value);
});

const handleChange = (e: any) => {
    emit('activeSubTabKeyOnChange', e)
    const selectedSubTab = props.newTabObject.find((subTab: any) => subTab.subTabKey === e);
    if(selectedSubTab){
        emit('emitCollapseObject', selectedSubTab.collapseObject)
        console.log("first",selectedSubTab.collapseObject)
    }else{
        console.error(`SubTab with key '${e}' not found.`);
    }
}

const emitChange = (e: any) => {
    collapseObject.value = e
    emit('emitCollapseObject', collapseObject.value)
}

</script>

<template>
    <div class="contentDiv">
        <a-tabs v-model:activeKey="activeKey" centered type="card" @change="handleChange">
            <a-tab-pane :key="props.subTabObject[0].subTabKey" :tab="props.subTabObject[0].subTabName">
                <CollapseComponent :subTabObject="props.subTabObject[0].subTabKey" :newTabObject="newTabObject[0]"
                    @emit-collapse-object="emitChange" />
            </a-tab-pane>
            <a-tab-pane :key="props.subTabObject[1].subTabKey" :tab="props.subTabObject[1].subTabName">
                <CollapseComponent :subTabObject="props.subTabObject[1].subTabKey" :newTabObject="newTabObject[1]"
                    @emit-collapse-object="emitChange" />
            </a-tab-pane>
            <a-tab-pane :key="props.subTabObject[2].subTabKey" :tab="props.subTabObject[2].subTabName">
                <CollapseComponent :subTabObject="props.subTabObject[2].subTabKey" :newTabObject="newTabObject[2]"
                    @emit-collapse-object="emitChange" />
            </a-tab-pane>
        </a-tabs>
    </div>
</template>

<style scoped>
.contentDiv {
    margin-bottom: 20px;
}
</style>