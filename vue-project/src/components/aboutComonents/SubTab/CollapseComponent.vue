<script setup lang="ts">
import { ref, onMounted, watchEffect } from 'vue';

const props = defineProps(['subTabObject', 'activeKeyOnChange', 'newTabObject'])

const emit = defineEmits(['emitCollapseObject'])

const activeKey = ref();

const text = `A dog is a type of domesticated animal.Known for its loyalty and faithfulness,it can be found as a welcome guest in many households across the world.`;

onMounted(() => {
    activeKey.value = props.newTabObject.collapseObject
    emit('emitCollapseObject', activeKey.value)
})

watchEffect(()=>{
    activeKey.value = props.newTabObject.collapseObject
})

const handleChange = (e: any) => {
    activeKey.value = e
    emit('emitCollapseObject', e)
}

</script>

<template>
    <div class="contentDiv">
        <a-collapse v-model:activeKey="activeKey" :expand-icon-position="'end'" @change="handleChange">
            <a-collapse-panel key="1" header="This is panel header 1">
                <p>{{ text }}</p>
            </a-collapse-panel>
            <a-collapse-panel key="2" header="This is panel header 2">
                <p>{{ text }}</p>
            </a-collapse-panel>
            <a-collapse-panel key="3" header="This is panel header 3">
                <p>{{ text }}</p>
            </a-collapse-panel>
        </a-collapse>
    </div>
</template>

<style scoped>
.contentDiv {
    margin-bottom: 20px;
}
</style>