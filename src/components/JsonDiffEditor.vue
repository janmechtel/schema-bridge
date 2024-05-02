
  <script setup lang="ts">
  import { defineProps} from 'vue';
  import { VueMonacoDiffEditor } from '@guolao/vue-monaco-editor';
  import * as monaco from 'monaco-editor/esm/vs/editor/editor.api';

  const OPTIONS: monaco.editor.IStandaloneEditorConstructionOptions = {
    automaticLayout: true,
    formatOnType: true,
    formatOnPaste: true,
    readOnly: false,
    language: "json",
    wordWrap: "on",
  };

  defineProps({
    original: String,
    modified: String,
  });

</script>
<template>
  <vue-monaco-diff-editor theme="vs-dark" :original="original" :modified="modified" :options="OPTIONS"
   />
</template>

