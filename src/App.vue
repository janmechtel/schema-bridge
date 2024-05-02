<script setup lang="ts">
import { loader } from '@guolao/vue-monaco-editor'
loader.config({
  paths: {
    vs: 'https://cdn.jsdelivr.net/npm/monaco-editor@0.43.0/min/vs',
  },
})

import jsonata from 'jsonata';
import { ref, watch, computed } from 'vue';

import Editor from './components/JsonEditor.vue';
import DiffEditor from './components/JsonDiffEditor.vue';

const jsonInput = ref(`{
  "id": "1001",
  "firstName": "Vinnie",
  "lastName": "Hickman",
  "age": 15,
  "country": "UK"
}`);
const jsonataExpression = ref(`{ 
  "id": id,
  "name" : firstName & " " & "try to include the last name here"
}`);
const transformationResult = ref('');
const jsonTargetOutput = ref(`{
  "id": "1001",
  "name": "Vinnie Hickman"
}`);

// Computed property to extract keys from jsonInput
const inputKeys = computed(() => {
  try {
    const json = JSON.parse(jsonInput.value);
    return Object.keys(json);
  } catch (error) {
    return [];
  }
});

const targetOutputKeys = computed(() => {
  try {
    const json = JSON.parse(jsonTargetOutput.value);
    return Object.keys(json);
  } catch (error) {
    return [];
  }
});
// Watch for changes in jsonInput or jsonataExpression and apply transformation
watch([jsonInput, jsonataExpression], () => {
  try {
    const json = JSON.parse(jsonInput.value);
    const expression = jsonata(jsonataExpression.value);
    expression.evaluate(json).then(result => {
      transformationResult.value = JSON.stringify(result, null, 2);
    });
  } catch (error) {
    if (error instanceof Error) {
      transformationResult.value = 'Error in transformation: ' + error.message;
    } else {
      transformationResult.value = "unknown type of the error " + error
    }
  }
}, { immediate: true });

</script>

<template>
  <h1>Schema-Bridge</h1>
  <div class="text-area-container">
    <div class="column">
      <h3>JSON Input</h3>
      <Editor v-model:value="jsonInput" />
      <h3>Input JSON Keys</h3>
      <ul>
        <li v-for="key in inputKeys" :key="key">{{ key }}</li>
      </ul>
    </div>
    <div class="column">
      <h3>JSONata Expression</h3>
      <Editor v-model:value="jsonataExpression" />
    </div>
    <div class="column double">
      <h3>Transformation Output & Target Output</h3>
      <DiffEditor :original="transformationResult" :modified="jsonTargetOutput" />
      <h3>Input JSON Keys</h3>
      <ul>
        <li v-for="key in targetOutputKeys" :key="key">{{ key }}</li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
.text-area-container {
  display: flex;
  height: 40vh;
  width: 100%;
}

.column {
  flex: 1;
  padding: 0 10px;
}

.double {
  flex: 2;
}

.column:first-child {
  padding-left: 0;
}

.column:last-child {
  padding-right: 0;
}
</style>
