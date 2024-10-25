<script setup>
import { ref } from 'vue';
import Form from './components/Form.vue';
import Card from './components/Card.vue';

const pacientes = ref([]);

function handleSubmit(formData) {
  pacientes.value.push(formData);
}

function removeCard(index) {
  pacientes.value.splice(index, 1);
}
</script>

<template>
  <Form @submitForm="handleSubmit" />  
  
  <div class="cards-container">
    <Card v-for="(paciente, index) in pacientes" :key="index" :data="paciente" @removeCard="removeCard" />
  </div>
</template>

<style scoped>
.cards-container {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  margin-top: 20px;
}
</style>

