<!-- App.vue -->
<template>
  <div id="app" class="container">
  <div class="row">
      <div class="col-md-12"><h1>Personas</h1></div>
  </div>
  <div class="row">
      <div class="col-md-12">
        <formulario-persona @add-persona="agregarPersona" />
        <tabla-personas :personas="personas" @delete-persona="eliminarPersona" />
      </div>
  </div>
  </div>
</template>

<script setup>
import TablaPersonas from '@/components/TablaPersonas.vue'
import FormularioPersona from '@/components/FormularioPersona.vue'
import { ref } from 'vue';

// definicion del componente
defineOptions({
// nombre del componente
name: 'app',
});

const personas = ref([]);

const agregarPersona = (persona) => {
  let id = 0;

  if (personas.value.length > 0) {
    id = personas.value[personas.value.length - 1].id + 1;
  }

  personas.value = [...personas.value, { ...persona, id }];
};

const eliminarPersona = (id) => {
  try {
    personas.value = personas.value.filter(
      (u) => u.id !== id
    );
  } catch (error) {
    console.error(error);
  }
};

const guardarPersona = (persona) => {
  if (!persona.nombre.length || !persona.apellido.length || !persona.email.length) {return;}
  emit('actualizar-persona', persona.id, persona);
  editando.value = null;
};

const cancelarEdicion = (persona) => {
  Object.assign(persona, personaEditada.value);
  editando.value = null;
};

</script>

<style>
  /* Estilos globales para todos los elementos button en la aplicacion */
  button {
  background: #009435;
  border: 1px solid #009435;
  }
</style>