<template>
  <div class="container">
    <form @submit.prevent="submitForm">
      <div class="info">
        <label for="paciente">Paciente</label>
        <input type="text" v-model="formData.paciente" id="paciente"/>
      </div>
      <div class="info">
        <label for="fecha">Fecha</label>
        <input type="date" v-model="formData.fecha" id="fecha"/>
      </div>
      <div class="info">
        <label for="hora">Hora</label>
        <input type="time" v-model="formData.hora" id="hora"/>
      </div>
      <div class="info">
        <label for="gravedad">Gravedad</label>
        <select v-model="formData.gravedad" id="gravedad">
          <option value="" disabled>Seleccione el nivel de gravedad</option>
          <option value="Baja">Baja</option>
          <option value="Media">Media</option>
          <option value="Alta">Alta</option>
        </select>
      </div>
      <div class="info">
        <label for="motivo">Motivo</label>
        <input type="text" v-model="formData.motivo" id="motivo"/>
      </div>
    </form>

    <div class="button">
        <button :disabled="!isFormComplete">Agregar</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Form",
  data() {
    return {
      formData: {
        paciente: "",
        fecha: "",
        hora: "",
        gravedad: "",
        motivo: "",
      },
      isFormComplete: false, // Nueva variable para habilitar/deshabilitar el botón
    };
  },
  methods: {
    submitForm() {
      this.updateFormStatus();
      if (this.isFormComplete) {
        this.$emit("submitForm", { ...this.formData });
        this.resetForm();
      }
    },
    updateFormStatus() {
      // Verifica si todos los campos tienen un valor no vacío
      this.isFormComplete = Object.values(this.formData).every(value => value !== "");
    },
    resetForm() {
      this.formData = {
        paciente: "",
        fecha: "",
        hora: "",
        gravedad: "",
        motivo: "",
      };
      this.isFormComplete = false; // Restablece el estado del botón
    },
  },
  watch: {
    formData: {
      handler: "updateFormStatus",
      deep: true, // Observa los cambios en cualquier campo del objeto formData
    },
  },
};
</script>

<style>
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
</style>
