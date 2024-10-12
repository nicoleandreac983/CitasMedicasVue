<script>
import CitaCard from './components/CitaCard.vue';

export default {
  name: 'AdmCitasMedicas',
  components: {
    CitaCard
  },
  data() {
    return {
      campos: [
        { nombre: 'Paciente', valor: '', tipo: 'text' },
        { nombre: 'Fecha', valor: '', tipo: 'date' },
        { nombre: 'Hora', valor: '', tipo: 'time' },
        { nombre: 'Gravedad', valor: '', tipo: 'select' }, 
        { nombre: 'Motivo', valor: '', tipo: 'text' },
      ],
      citas: [],
      formularioValido: false,
    };
  },
  methods: {
    validarFormulario() {
 
      this.formularioValido = this.campos.every(campo => campo.valor !== '');
    },
    agregarCita() {
      // Recoge los valores de los campos
      const nuevaCita = {
        paciente: this.campos[0].valor,
        fecha: this.campos[1].valor,
        hora: this.campos[2].valor,
        gravedad: this.campos[3].valor, 
        motivo: this.campos[4].valor,
      };
    
      this.citas.push(nuevaCita);
      this.limpiarFormulario();
    },
    limpiarFormulario() {
      
      this.campos.forEach(campo => (campo.valor = ''));
      this.formularioValido = false;
    },
    eliminarCita(index) {

      this.citas.splice(index, 1);
    },
  },
};
</script>


<template>
  <div id="app">
    <h1>Administrador de Citas Médicas</h1>
    <form @submit.prevent="agregarCita">
      <div v-for="(campo, index) in campos" :key="index">
        <label :class="{ rojo: !campo.valor }">{{ campo.nombre }}</label>
        <div v-if="campo.nombre === 'Gravedad'">
          <select v-model="campo.valor" @input="validarFormulario">
            <option disabled value="">Selecciona una gravedad</option>
            <option value="baja">Baja</option>
            <option value="media">Media</option>
            <option value="alta">Alta</option>
          </select>
        </div>
        <div v-else>
          <input v-model="campo.valor" @input="validarFormulario" :type="campo.tipo" />
        </div>
      </div>
      <button :disabled="!formularioValido">Agregar Cita</button>
    </form>
    <p class="mensaje" v-if="citas.length === 0">Aún no hay consultas registradas.</p>
    <div v-else>
      <CitaCard 
        v-for="(cita, index) in citas" 
        :key="index" 
        :cita="cita"  
        @eliminar-cita="eliminarCita(index)"  />

    </div>
  </div>
</template>


<style scoped>
h1 {
  text-align: center;
}

.mensaje {
  text-align: center;
  margin-top: 20px;
  font-weight: bold;
}

form{
  border: 1px solid #cdb3d2cc;
  border-radius: 10px; 
  padding: 20px; 
  max-width: 400px; 
  margin: auto; 
  background-color: #cdb3d2cc;
}

.campo {
  margin-bottom: 15px;
}

label {
  display: block; 
  margin-bottom: 5px; 
}

select {
  width: 100%; 
  padding: 8px; 
  border: 1px solid #ccc; 
  border-radius: 5px; 
}

button {
  padding: 10px 15px; 
  border: none; 
  border-radius: 5px; 
  background-color: #4CAF50; 
  color: white; 
  cursor: pointer; 
}
button:disabled {
  background-color: #ccc;
}
.rojo {
  color: red;
}
</style>