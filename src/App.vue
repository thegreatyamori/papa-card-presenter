<template>
  <div id="app">
    <header class="header-bar">
      <input
        v-model="inputIds"
        placeholder="Ingresa IDs separados por coma (ej: 1,3,5)"
        class="search-input"
        @keydown.enter="searchQuestions"
      />
      <button @click="searchQuestions" class="search-button">Buscar</button>
    </header>
    <main class="cards-container">
      <div v-if="questions.length" class="cards-grid">
        <div v-for="q in questions" :key="q.id" class="card">
          <div class="card-content">
            <div
              class="category"
              :style="{ backgroundColor: getCategoryColor(q.category) }"
            >
              {{ q.category }}
            </div>
            <div class="question">{{ q.question }}</div>
            <div class="id">{{ q.id }}</div>
          </div>
        </div>
      </div>
      <p v-else-if="searched" class="no-results">No se encontraron preguntas</p>
    </main>
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
        .slice(0, 5);
      this.searched = true;
    },
    getCategoryColor(category) {
      const colors = [
        "#ff6b6b",
        "#4ecdc4",
        "#ffe66d",
        "#a8e6cf",
        "#dda0dd",
        "#98fb98",
        "#ffb6c1",
        "#87ceeb",
        "#f0e68c",
      ];
      let hash = 0;
      for (let i = 0; i < category.length; i++) {
        hash = category.charCodeAt(i) + ((hash << 5) - hash);
      }
      return colors[Math.abs(hash) % colors.length];
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

.header-bar {
  display: flex;
  align-items: center;
  padding: 10px 20px;
  background: rgba(255, 255, 255, 0.9);
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
}

.search-input {
  flex: 1;
  padding: 15px 20px;
  border: 2px solid #ff6b6b;
  border-radius: 25px;
  font-family: "Roboto", sans-serif;
  font-size: 24px;
  font-weight: 500;
  margin-right: 10px;
  outline: none;
  transition: border-color 0.3s;
}

.search-input:focus {
  border-color: #4ecdc4;
}

.search-button {
  padding: 15px 30px;
  background: #ffe66d;
  border: none;
  border-radius: 25px;
  font-family: "Roboto", sans-serif;
  font-size: 20px;
  font-weight: 500;
  color: #333;
  cursor: pointer;
  transition: background 0.3s;
}

.search-button:hover {
  background: #ffd93d;
}

.cards-container {
  flex: 1;
}

.cards-grid {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  gap: 20px;
  height: auto;
  width: 100%;
  padding-top: 2%;
}

.card {
  background: url("https://cdn.wellpapers.com/wp-content/uploads/2024/10/n648-motif-600x902.jpg")
    repeat;
  background-size: 300px 400px;
  border-radius: 15px;
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.3),
    inset 0 0 20px rgba(255, 255, 255, 0.5); /* Sombra y brillito */
  overflow: hidden;
  position: relative;
  width: 275px;
  height: 300px;
  transform: rotate(-1deg); /* Ligero giro para apariencia de carta */
  transition: transform 0.3s;
}

.card:hover {
  transform: rotate(0deg) scale(1.05);
}

.card-content {
  padding: 20px 0;
  background: rgb(255 255 255 / 85%);
  border-radius: 20px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  word-wrap: break-word;
  white-space: pre-wrap;
}

.category {
  position: absolute;
  top: 10px;
  left: 50%;
  transform: translateX(-50%);
  font-size: 24px;
  font-weight: bold;
  color: #333;
  padding: 5px 10px;
  border-radius: 5px;
}

.question {
  text-align: center;
  font-size: 28px;
  color: #333;
  margin: 20px 0;
}

.id {
  position: absolute;
  bottom: 10px;
  right: 10px;
  font-size: 25px;
  color: black;
}

.no-results {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-size: 64px;
  color: black;
  background: white;
  padding: 40px;
  border-radius: 20px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
  text-align: center;
}
</style>

<style>
body {
  margin: 0;
}
</style>
