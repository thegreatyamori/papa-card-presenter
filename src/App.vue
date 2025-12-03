<template>
  <div id="app">
    <HeaderBar
      :input-ids="inputIds"
      @update:input-ids="inputIds = $event"
      @search="searchQuestions"
    />
    <CardsGrid :questions="questions" :searched="searched" />
  </div>
</template>

<script>
import Papa from "papaparse";
import HeaderBar from "./components/HeaderBar.vue";
import CardsGrid from "./components/CardsGrid.vue";

export default {
  components: {
    HeaderBar,
    CardsGrid,
  },
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
        .slice(0, 5);
      this.searched = true;
    },
  },
};
</script>

<style scoped>
#app {
  font-family: "Roboto", sans-serif;
  font-weight: 500; /* Medium para legibilidad y grosor */
  background: linear-gradient(
    135deg,
    #ff6b6b,
    #4ecdc4,
    #ffe66d,
    #a8e6cf
  ); /* Paleta viva */
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}
</style>

<style>
body {
  margin: 0;
}
</style>
