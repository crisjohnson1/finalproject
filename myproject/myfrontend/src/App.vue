<!-- App.vue -->
<template>
  <div id="app">
    <header>
      <button @click="showPage('list')">Lista de Personas</button>
      <button @click="showPage('create')">Crear Persona</button>
    </header>
    <main>
      <component :is="currentPage"></component>
    </main>
  </div>
</template>

<script>
import PersonaList from './components/PersonaList.vue';
import PersonaForm from './components/PersonaForm.vue';

export default {
  name: 'App',
  components: {
    PersonaList,
    PersonaForm
  },
  data() {
    return {
      currentPage: 'PersonaList' // Página inicial
    };
  },
  methods: {
    showPage(pageName) {
      this.currentPage = pageName;
    }
  }
};
</script>
