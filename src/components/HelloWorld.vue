<script setup lang="ts">
import { ref } from 'vue'

defineProps<{ msg: string }>()

const count = ref(0)
</script>

<template>
  <h1>{{ msg }}</h1>

  <div class="card">
    <button type="button" @click="count++">count is {{ count }}</button>
    <p>
      Edit
      <code>components/HelloWorld.vue</code> to test HMR
    </p>
  </div>
  <p>
    Special Thanks
    <a href="https://www.youtube.com/watch?v=-kZLD40d-tI" target="_blank"
      >Adding Drag and Drop to Your Vue 3 Project</a
    >
  </p>
</template>

<style scoped>

</style>
