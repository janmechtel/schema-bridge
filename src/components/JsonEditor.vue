<script setup lang="ts">

import { VueMonacoEditor } from '@guolao/vue-monaco-editor'
const model = defineModel<string | undefined>()


const MONACO_EDITOR_OPTIONS = {
  automaticLayout: true,
  formatOnType: true,
  formatOnPaste: true,
  minimap: {
    enabled: false
  },
}


</script>

<template>
  <VueMonacoEditor
    v-model:value="model" 
    theme="vs-dark"
    language="json"
    :options="MONACO_EDITOR_OPTIONS"  
  />
</template>

<style scoped></style>
