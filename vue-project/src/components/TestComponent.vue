<script setup lang="ts">

const props = defineProps({
    title: String
}) 


</script>

<template>
    <div>
        <h1>TABLE {{ props.title }}</h1>
    </div>
</template>
  
<style>
@media (min-width: 1024px) {
    .about {
        min-height: 100vh;
        display: flex;
        align-items: center;
    }
}
</style>
  