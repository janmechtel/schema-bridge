<script setup lang="ts">

import { VueMonacoEditor } from '@guolao/vue-monaco-editor'
import * as monaco from 'monaco-editor/esm/vs/editor/editor.api';
const model = defineModel<string | undefined>()


const OPTIONS: monaco.editor.IStandaloneEditorConstructionOptions = {
  automaticLayout: true,
  formatOnType: true,
  formatOnPaste: true,
  minimap: {
    enabled: false
  },
  wordWrap: "on",
}


</script>

<template>
  <VueMonacoEditor
    v-model:value="model" 
    theme="vs-dark"
    language="json"
    :options="OPTIONS"  
  />
</template>
