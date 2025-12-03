<template>
  <div id="app">
    <h1>Papa Card Presenter</h1>
    <input
      v-model="inputIds"
      placeholder="Ingresa IDs separados por coma (ej: 1,3,5)"
    />
    <button @click="searchQuestions">Buscar</button>
    <ul v-if="questions.length">
      <li v-for="q in questions" :key="q.id">{{ q.question }}</li>
    </ul>
    <p v-else-if="searched">No se encontraron preguntas.</p>
  </div>
</template>

<script>
import Papa from "papaparse";

export default {
  data() {
    return {
      inputIds: "",
      questions: [],
      allQuestions: [],
      searched: false,
    };
  },
  mounted() {
    this.loadCSV();
  },
  methods: {
    loadCSV() {
      Papa.parse("/questions.csv", {
        download: true,
        header: true,
        complete: (results) => {
          this.allQuestions = results.data;
        },
      });
    },
    searchQuestions() {
      const ids = this.inputIds
        .split(",")
        .map((id) => id.trim())
        .filter((id) => id);
      this.questions = this.allQuestions
        .filter((q) => ids.includes(q.id))
        .slice(0, 4);
      this.searched = true;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
