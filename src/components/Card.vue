<template>
  <div class="card" :style="{ backgroundColor: backgroundColor }">
    <h3>{{ data.paciente }}</h3>
    <p><strong>Fecha:</strong> {{ data.fecha }}</p>
    <p><strong>Hora:</strong> {{ data.hora }}</p>
    <p><strong>Motivo:</strong> {{ data.motivo }}</p>
    <p><strong>Gravedad:</strong> {{ data.gravedad }}</p>

    <!-- Botón para eliminar la tarjeta -->
    <button @click="removeCard">Eliminar</button>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: {
    data: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      backgroundColor: "white", // Valor predeterminado
    };
  },
  watch: {
    data: {
      immediate: true,
      handler(newData) {
        this.setBackgroundColor(newData.gravedad);
      },
    },
  },
  methods: {
    setBackgroundColor(gravedad) {
      if (gravedad === "Baja") {
        this.backgroundColor = "lightgreen";
      } else if (gravedad === "Media") {
        this.backgroundColor = "yellow";
      } else if (gravedad === "Alta") {
        this.backgroundColor = "lightcoral";
      }
    },
    removeCard() {
      // Emite el evento `removeCard` al componente padre
      this.$emit("removeCard", this.data.id);
    },
  },
};
</script>

<style scoped>
.card {
  padding: 1rem;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  width: 200px;
}

button {
  margin-top: 10px;
  padding: 0.5rem;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
</style>
