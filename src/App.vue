<script setup lang="ts">
import { loader } from '@guolao/vue-monaco-editor'
loader.config({
  paths: {
    vs: 'https://cdn.jsdelivr.net/npm/monaco-editor@0.43.0/min/vs',
  },
})

import jsonata from 'jsonata';
import { ref, watch, computed, onMounted } from 'vue';

import Editor from './components/JsonEditor.vue';
import DiffEditor from './components/JsonDiffEditor.vue';

const jsonInput = ref(localStorage.getItem('jsonInput') || `{
  "id": "1001",
  "firstName": "Vinnie",
  "lastName": "Hickman",
  "age": 15,
  "country": "UK"
}`);
const jsonataExpression = ref(localStorage.getItem('jsonataExpression') || `{ 
  "id": id,
  "name" : firstName & " " & "try to include the last name here"
}`);
const transformationResult = ref('');
const jsonTargetOutput = ref(localStorage.getItem('jsonTargetOutput') || `{
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

// Computed property to extract keys from jsonataExpression               
const expressionKeys = computed(() => {
  const lines = jsonataExpression.value.split('\n').slice(1, -1); // Ignore the first and last lines
  return lines.map(line => {
    const key = line.split(':')[0].trim(); // Get the part before the first colon
    return key.replace(/["']/g, ''); // Remove quotes                     
  });
});

// Save to local storage
const saveToLocalStorage = (key: any, value: any) => {
  localStorage.setItem(key, value);
};

// Watchers to save data to local storage
watch(jsonInput, (newValue) => {
  saveToLocalStorage('jsonInput', newValue);
}, { immediate: true });

watch(jsonataExpression, (newValue) => {
  evaluateExpression()
  saveToLocalStorage('jsonataExpression', newValue);
}, { immediate: true });

watch(jsonTargetOutput, (newValue) => {
  evaluateExpression()
  saveToLocalStorage('jsonTargetOutput', newValue);
}, { immediate: true });

// Watch for changes in jsonInput or jsonataExpression and apply transformation
function evaluateExpression() {
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
}

// Load from local storage
onMounted(() => {
  jsonInput.value = localStorage.getItem('jsonInput') || jsonInput.value;
  jsonataExpression.value = localStorage.getItem('jsonataExpression') || jsonataExpression.value;
  jsonTargetOutput.value = localStorage.getItem('jsonTargetOutput') || jsonTargetOutput.value;
});

// Computed properties and other code remains unchanged
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
      <h3>Expression Keys</h3>
      <ul>
        <li v-for="key in expressionKeys" :key="key">{{ key }}</li>
      </ul>
    </div>
    <div class="column, double">
      <h3>Transformation Output & Target Output</h3>
      <DiffEditor :original="transformationResult" :modified="jsonTargetOutput" />
      <h3>Target Output JSON Keys</h3>
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
