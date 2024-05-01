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
  <div class="text-area-container">
    <textarea v-model="jsonInput" placeholder="Enter JSON here..."></textarea>
    <textarea v-model="jsonataExpression" placeholder="Enter JSONata expression here..."></textarea>
    <textarea v-model="transformationResult" placeholder="Transformation result" readonly></textarea>
  </div>
</template>

<style scoped>
.text-area-container {
  display: flex;
  height:95vh;
}
textarea {
  flex: 1;
  margin: 0 10px;
  padding: 8px;
  box-sizing: border-box;
  border: 1px solid #ccc;
  border-radius: 4px;
}
</style>






