<script setup lang="ts">
import { RouterView } from 'vue-router'
</script>

<template>
  <nav>
    <a-row :gutter="16">
      <a-col class="gutter-row" :span="12">
        <div class="gutter-box">
          <router-link to="/about">Go to test page</router-link>
        </div>
      </a-col>
      <a-col class="gutter-row" :span="12">
        <div class="gutter-box">
          <router-link to="/">Go to main page</router-link>
        </div>
      </a-col>
    </a-row>
  </nav>
  <RouterView />
</template>

<style scoped>
nav a.router-link-exact-active {
  color: var(--color-text);
}
</style>