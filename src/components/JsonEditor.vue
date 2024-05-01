<script setup lang="ts">

import JsonEditorVue from 'json-editor-vue'
const model = defineModel()

</script>

<template>
  <JsonEditorVue 
    v-model="model" 
    v-bind="{/* local props & attrs */ }" 
    :stringified="false" 
    mode="text"/>
</template>

<style scoped></style>
