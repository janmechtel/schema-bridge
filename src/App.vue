<script setup lang="ts">
import jsonata from 'jsonata';
import { ref, watch } from 'vue';

import Editor from './components/Editor.vue';
  
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
}
`);  // Initialize the new reactive variable for JSON Target Output

// Watch for changes in jsonInput or jsonataExpression and apply transformation
watch([jsonInput, jsonataExpression], () => {
  try {
    const json = JSON.parse(jsonInput.value);
    const expression = jsonata(jsonataExpression.value);
    expression.evaluate(json).then(result => {
      transformationResult.value = JSON.stringify(result, null, 2);;
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
      <Editor v-model="jsonInput" />
    </div>
    <div class="column">
      <h3>JSONata Expression</h3>
      <Editor v-model="jsonataExpression" />
    </div>
    <div class="column">
      <h3>Transformation Result</h3>
      <Editor v-model="transformationResult" />
    </div>
    <div class="column">
      <h3>JSON Target Output</h3>
      <Editor v-model="jsonTargetOutput" />
    </div>
  </div>
</template>

<style scoped>
.text-area-container {
  display: flex;
  height: 100vh;
  width: 100%;
}
.column {
  flex: 1;
  padding: 0 10px;
}
.column:first-child {
  padding-left: 0;
}
.column:last-child {
  padding-right: 0;
}
</style>







