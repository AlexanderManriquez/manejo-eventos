<template>
    <div class="container">
      <form @submit.prevent="submitForm">
        <div class="info">
          <label :for="'paciente'" :class="labelClass(formData.paciente)">Paciente</label>
          <input type="text" v-model="formData.paciente" id="paciente"/>
        </div>
        <div class="info">
          <label :for="'fecha'" :class="labelClass(formData.fecha)">Fecha</label>
          <input type="date" v-model="formData.fecha" id="fecha"/>
        </div>
        <div class="info">
          <label :for="'hora'" :class="labelClass(formData.hora)">Hora</label>
          <input type="time" v-model="formData.hora" id="hora"/>
        </div>
        <div class="info">
          <label :for="'gravedad'" :class="labelClass(formData.gravedad)">Gravedad</label>
          <select v-model="formData.gravedad" id="gravedad">
            <option value="" disabled>Seleccione el nivel de gravedad</option>
            <option value="Baja">Baja</option>
            <option value="Media">Media</option>
            <option value="Alta">Alta</option>
          </select>
        </div>
        <div class="info">
          <label :for="'motivo'" :class="labelClass(formData.motivo)">Motivo</label>
          <input type="text" v-model="formData.motivo" id="motivo"/>
        </div>
      </form>
  
      <div class="button">
          <button :disabled="!isFormComplete" @click="submitForm">Agregar</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        formData: {
          paciente: "",
          fecha: "",
          hora: "",
          gravedad: "",
          motivo: "",
        },
      };
    },
    computed: {
    //Propiedad computada que nos permite verificar si todos los campos del formulario estan llenos
      isFormComplete() {
        return Object.values(this.formData).every(value => value !== "");
      },
    },
    methods: {
    
      submitForm() {
        if (this.isFormComplete) {
          this.$emit("submitForm", { ...this.formData });
          this.resetForm();
        }
      },
      resetForm() {
        this.formData = {
          paciente: "",
          fecha: "",
          hora: "",
          gravedad: "",
          motivo: "",
        };
      },
      labelClass(value) {
        return value ? "filled" : "empty"; // aplica la clase respectiva para modificar el color del texto de cada label
      },
    },
  };
  </script>
  
  <style scoped>
  .container {
    border: 2px solid gray;
    border-radius: 25px;
    padding: 1rem;
  }
  
  form {
    display: flex;
  }
  
  .info {
    display: flex;
    flex-direction: column;
    margin: 10px;
  }
  
  .empty {
    color: red;
  }
  
  .filled {
    color: black;
  }
  
  .button {
    margin-top: 10px;
  }
  </style>
  