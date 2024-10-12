<script>
  export default {
    props: ['cita'], // Recibe la cita desde el componente padre
    computed: {
      // Cambia el color de fondo según la gravedad
      colorGravedad() {
        switch (this.cita.gravedad.toLowerCase()) {
          case 'baja':
            return 'green';
          case 'media':
            return 'yellow';
          case 'alta':
            return 'red';
          default:
            return 'white';
        }
      },
    },
    methods: {
      emitirEliminar() {
        // Emite el evento para eliminar la cita
        this.$emit('eliminar-cita');
      },

    },
  };
  </script>
<template>
    <div :style="{ backgroundColor: colorGravedad, textAlign: 'center' }" class="cita-card">
      <h3>Paciente</h3>
      <p>{{ cita.paciente }}</p>
      <h3>Fecha</h3>
      <p> {{ cita.fecha }}</p>
      <h3>Hora</h3>
      <p>{{ cita.hora }}</p>
      <h3>Gravedad</h3>
      <p>{{ cita.gravedad }}</p>
      <h3>Motivo</h3>
      <p>{{ cita.motivo }}</p>
      <button @click="emitirEliminar">Eliminar</button>
    </div>
  </template>
  
  <style scoped>
  .cita-card {
    border: 1px solid #ccc;
    padding: 16px;
    margin: 16px 0;
    border-radius: 8px;
    width: 200px;
    height: auto;
  }
  </style>
  
  