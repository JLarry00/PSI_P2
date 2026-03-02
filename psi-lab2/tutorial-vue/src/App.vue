<!-- -->
<template>
  <div
    id="app"
    class="container"
  >
    <div class="row">
      <div class="col-md-12">
        <h1>Personas</h1>
      </div>
    </div>
    <div class="row">
      <div class="col-md-12">
        <formulario-persona @add-persona="agregarPersona" />
        <tabla-personas
          :personas="personas"
          @delete-persona="eliminarPersona"
          @actualizar-persona="actualizarPersona"
        />
      </div>
    </div>
  </div>
</template>

<script setup>
  import TablaPersonas from '@/components/TablaPersonas.vue'
  import FormularioPersona from '@/components/FormularioPersona.vue'
  import { ref, onMounted } from 'vue';
  // import { useCounterStore } from '@/stores/counter'; // usar en método correspondiente

  const API_URL = 'http://localhost:8001/api/v1/personas/';

  defineOptions({
    name: 'app',
  });

  const personas = ref([]);

  const listadoPersonas = async () => {
    // Metodo para obtener un listado de personas
    try {
      const response = await fetch(API_URL);
      personas.value = await response.json();
    } catch (error) {
      console.error(error);
    }      
  };

  const agregarPersona = async (persona) => {
    try {
      const response = await fetch(API_URL, {
        method: 'POST',
        body: JSON.stringify(persona),
        headers: { 'Content-type': 'application/json; charset=UTF-8' },
      });
      
      const personaCreada = await response.json();
      if (!response.ok) {
        console.error('Error al agregar la persona', personaCreada);
        return;
      }
      personas.value = [...personas.value, personaCreada];
      
    } catch (error) {
      console.error(error);
    }
  };

  const eliminarPersona = async (persona_id) => {
    // Metodo para eliminar una persona
    try {
      await fetch(API_URL + persona_id + '/', {
        method: "DELETE"
      });
      
      personas.value= personas.value.filter(u => u.id !== persona_id);
    } catch (error) {
      console.error(error);
    }      
  };

  const actualizarPersona = async (id, personaActualizada) => {
    // Metodo para actualizar una persona
    try {
        const response = await fetch(API_URL + personaActualizada.id + '/', {
            method: 'PUT',
            body: JSON.stringify(personaActualizada),
              headers: { 'Content-type': 'application/json; charset=UTF-8' },
            });

        const personaActualizadaJS = await response.json();
        personas.value = personas.value.map(u => (u.id === personaActualizada.id ? personaActualizadaJS : u));         
    } catch (error) {
      console.error(error);
    }      
  };

  // Fetch data when the component is mounted
  onMounted(() => {
    listadoPersonas();
  });
</script>

<style>
  button {
    background: #009435;
    border: 1px solid #009435;
  }
</style>