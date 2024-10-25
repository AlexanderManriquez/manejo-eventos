<template>
  <Form @submitForm="handleSubmit" />

  <div class="cards-container">
    <p v-if="pacientes.length === 0" class="no-citas">No hay citas ingresadas</p>
    <Card v-for="(paciente, index) in pacientes" :key="index" :data="paciente" @removeCard="removeCard(index)" />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import Form from './components/Form.vue';
import Card from './components/Card.vue';

const pacientes = ref([]);

const handleSubmit = formData => pacientes.value.push(formData);

const removeCard = index =>  pacientes.value.splice(index, 1);
</script>

<style scoped>
.cards-container {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  margin-top: 20px;
}

.no-citas {
  color: red;
  font-size: 1.2rem;
  display: block;
  margin: 0 auto;
}
</style>


