<template>
    <div>
      <h1>Personas</h1>
      <ul>
        <li v-for="persona in personas" :key="persona.id">
          {{ persona.nombres }} {{ persona.apellidos }}
          <button @click="editPersona(persona.id)">Editar</button>
          <button @click="deletePersona(persona.id)">Eliminar</button>
        </li>
      </ul>
      <button @click="createPersona">Crear Persona</button>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        personas: []
      }
    },
    methods: {
      fetchPersonas() {
        this.$http.get('personas/')
          .then(response => {
            this.personas = response.data;
          });
      },
      createPersona() {
        this.$router.push({ name: 'createPersona' });
      },
      editPersona(id) {
        this.$router.push({ name: 'editPersona', params: { id } });
      },
      deletePersona(id) {
        this.$http.delete(`personas/${id}/`)
          .then(() => {
            this.fetchPersonas();
          });
      }
    },
    created() {
      this.fetchPersonas();
    }
  }
  </script>
  