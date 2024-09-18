<script setup>
import { ref } from 'vue'

defineProps({
  msg: String,
})

const count = ref(0)
</script>

<template>
  <h1 class="read-the-docs">Я Ткачнеок Iван</h1>

  <p class="read-the-docs">
    Я делать лаба, устать
  </p>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
