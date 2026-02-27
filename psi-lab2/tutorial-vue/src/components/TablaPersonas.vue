<!-- src/components/TablaPersonas.vue -->
<template>
  
  <div id="tabla-personas">

    <div v-if="!personas.length" class="alert alert-info" role="alert">
      No se han encontrado personas
    </div>

    <table class="table">
      <thead>
        <tr>
          <th>Nombre</th>
          <th>Apellido</th>
          <th>Email</th>
          <th>Acciones</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="persona in personas" :key="persona.id">
          <td>{{ persona.nombre }}</td>
          <td>{{ persona.apellido }}</td>
          <td>{{ persona.email }}</td>
          <td>
            <!-- &#x1F5D1; is the wastebasket icon. Icons available at https://codepoints.net -->
            <button class="btn btn-danger" @click="$emit('delete-persona', persona.id)" >&#x1F5D1; Eliminar</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
  defineOptions({
    name: 'tabla-personas',
  });

  const props = defineProps({
    personas: {type: Array, default: []},
  });
</script>

<style scoped>
  /* Estilos especificos del componente con el modificador "scoped" */
</style>