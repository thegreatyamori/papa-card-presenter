<template>
  <div id="app">
    <HeaderBar
      :input-ids="inputIds"
      @update:input-ids="inputIds = $event"
      @search="searchQuestions"
      :show-view-all="!showAllCards"
      @view-all="viewAllCards"
      :show-back="showAllCards"
      @back="backToSearch"
    />
    <CardsGrid
      v-if="!showAllCards"
      :questions="questions"
      :searched="searched"
    />
    <PrintView v-if="showAllCards" :grouped-questions="groupedQuestions" />
  </div>
</template>

<script>
import Papa from "papaparse";
import HeaderBar from "./components/HeaderBar.vue";
import CardsGrid from "./components/CardsGrid.vue";
import PrintView from "./components/PrintView.vue";
import Card from "./components/Card.vue";

export default {
  components: {
    HeaderBar,
    CardsGrid,
    PrintView,
    Card,
  },
  data() {
    return {
      inputIds: "",
      questions: [],
      allQuestions: [],
      searched: false,
      showAllCards: false,
    };
  },
  mounted() {
    this.loadCSV();
  },
  computed: {
    groupedQuestions() {
      return this.chunkArray(this.allQuestions, 15);
    },
  },
  methods: {
    loadCSV() {
      Papa.parse("/questions.csv", {
        download: true,
        header: true,
        complete: (results) => {
          this.allQuestions = results.data.filter((q) => q.id && q.question);
        },
      });
    },
    searchQuestions() {
      const ids = this.inputIds
        .split(",")
        .map((id) => id.trim())
        .filter((id) => id);
      console.log("Searching for IDs:", ids);
      console.log(this.allQuestions);

      this.questions = this.allQuestions.filter((q) => ids.includes(q.id));
      this.searched = true;
    },
    viewAllCards() {
      this.showAllCards = true;
    },
    backToSearch() {
      this.showAllCards = false;
      this.questions = [];
      this.searched = false;
    },
    chunkArray(array, size) {
      const chunked = [];
      for (let i = 0; i < array.length; i += size) {
        chunked.push(array.slice(i, i + size));
      }
      return chunked;
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

@page {
  size: A4 landscape;
  margin: 0 5mm 0 0;
  -webkit-print-color-adjust: exact;
  color-adjust: exact;
}

@media print {
  .header-bar {
    display: none !important;
  }
  .print-view {
    background: white !important;
  }
}
</style>
