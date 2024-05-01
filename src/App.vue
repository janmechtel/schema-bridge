<script setup lang="ts">
import jsonata from 'jsonata';
import { ref } from 'vue';

const jsonInput = ref('{ "name": "Wilbur" }');
const greeting = ref('');

function handleGreeting() {
  const json = JSON.parse(jsonInput.value);
  const expression = jsonata('"Hello, " & name');
  expression.evaluate(json).then(result => {
    greeting.value = result;
  });
}
</script>

<template>
  <textarea v-model="jsonInput" placeholder="Enter JSON here..."></textarea>
  <button @click="handleGreeting">Click me</button>
  <p>{{ greeting }}</p>
</template>

<style scoped>
textarea {
  width: 100%;
  height: 100px;
  margin-bottom: 10px;
  padding: 8px;
  box-sizing: border-box;
  border: 1px solid #ccc;
  border-radius: 4px;
}
button {
  padding: 10px 20px;
  border-radius: 4px;
  cursor: pointer;
}
</style>




