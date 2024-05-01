<script setup lang="ts">

const model = defineModel()

</script>

<template>
  <textarea v-model="model" placeholder="Enter text here..."></textarea>
</template>

<style scoped>
textarea {
  width: 100%;
  height: 100%;
  padding: 8px;
  box-sizing: border-box;
  border: 1px solid #ccc;
  border-radius: 4px;
}
</style>
