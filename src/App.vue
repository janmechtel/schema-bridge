<script setup lang="ts">
import jsonata from 'jsonata';
import { ref, watch } from 'vue';

const jsonInput = ref('{ "name": "Wilbur" }');
const jsonataExpression = ref('"Hello, " & name');
const transformationResult = ref('');

// Watch for changes in jsonInput or jsonataExpression and apply transformation
watch([jsonInput, jsonataExpression], () => {
  try {
    const json = JSON.parse(jsonInput.value);
    const expression = jsonata(jsonataExpression.value);
    expression.evaluate(json).then(result => {
      transformationResult.value = result;
    });
  } catch (error) {
    transformationResult.value = 'Error in transformation: ' + error.message;
  }
}, { immediate: true });

</script>

<template>
  <h1>Schema-Bridge</h1>
  <div class="text-area-container">
    <div class="column">
      <h3>JSON Input</h3>
      <textarea v-model="jsonInput" placeholder="Enter JSON here..."></textarea>
    </div>
    <div class="column">
      <h3>JSONata Expression</h3>
      <textarea v-model="jsonataExpression" placeholder="Enter JSONata expression here..."></textarea>
    </div>
    <div class="column">
      <h3>Transformation Result</h3>
      <textarea v-model="transformationResult" placeholder="Transformation result" readonly></textarea>
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
textarea {
  width: 100%;
  height: 90%; /* Adjusted to leave space for headers */
  padding: 8px;
  box-sizing: border-box;
  border: 1px solid #ccc;
  border-radius: 4px;
}
h1, h3 {
  margin-bottom: 10px;
}
</style>





