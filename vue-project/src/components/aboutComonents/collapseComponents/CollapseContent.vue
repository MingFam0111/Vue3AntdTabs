<script lang="ts" setup>
import { ref, watchEffect } from 'vue';

const props = defineProps([
    'collapseKey'
])

const emit = defineEmits(['childCollapseKey'])

const text = `A dog is a type of domesticated animal.Known for its loyalty and faithfulness,it can be found as a welcome guest in many households across the world.`;
const activeKey = ref(props.collapseKey);


watchEffect(() => {
    activeKey.value = props.collapseKey
    console.log(props.collapseKey)
})

const changeActivekey = (key: string) => {
  console.log(key, " HELLO ");
  emit('childCollapseKey', key)
};

</script>

<template>
    <a-collapse v-model:activeKey="activeKey" @change="changeActivekey">
        <a-collapse-panel key="1" header="This is panel header 1">
            <p>{{ text }}</p>
        </a-collapse-panel>
        <a-collapse-panel key="2" header="This is panel header 1">
            <p>{{ text }}</p>
        </a-collapse-panel>
        <a-collapse-panel key="3" header="This is panel header 1">
            <p>{{ text }}</p>
        </a-collapse-panel>
    </a-collapse>
</template>