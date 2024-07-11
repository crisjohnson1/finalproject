<template>
    <div>
      <h1>{{ isEditMode ? 'Editar' : 'Crear' }} Persona</h1>
      <form @submit.prevent="savePersona">
        <div>
          <label>Nombres</label>
          <input v-model="persona.nombres" required>
        </div>
        <div>
          <label>Apellidos</label>
          <input v-model="persona.apellidos" required>
        </div>
        <!-- Añade los demás campos aquí -->
        <button type="submit">Guardar</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        persona: {
          nombres: '',
          apellidos: '',
          // Añade los demás campos aquí
        },
        isEditMode: false
      }
    },
    methods: {
      fetchPersona(id) {
        this.$http.get(`personas/${id}/`)
          .then(response => {
            this.persona = response.data;
            this.isEditMode = true;
          });
      },
      savePersona() {
        if (this.isEditMode) {
          this.$http.put(`personas/${this.persona.id}/`, this.persona)
            .then(() => {
              this.$router.push({ name: 'personas' });
            });
        } else {
          this.$http.post('personas/', this.persona)
            .then(() => {
              this.$router.push({ name: 'personas' });
            });
        }
      }
    },
    created() {
      if (this.$route.params.id) {
        this.fetchPersona(this.$route.params.id);
      }
    }
  }
  </script>
  