<template>
  <div class="cards-container">
    <div v-if="questions.length" class="cards-grid">
      <Card
        v-for="q in questions"
        :key="q.id"
        :question="q"
        @select="selectCard"
      />
    </div>
    <NoResults v-if="!questions.length && searched" />

    <transition name="fade">
      <div
        v-if="selectedQuestion"
        class="overlay"
        @click="selectedQuestion = null"
      >
        <div class="enlarged-card">
          <Card :question="selectedQuestion" :clickable="false" />
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
import Card from "./Card.vue";
import NoResults from "./NoResults.vue";

export default {
  components: {
    Card,
    NoResults,
  },
  props: {
    questions: {
      type: Array,
      default: () => [],
    },
    searched: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      selectedQuestion: null,
    };
  },
  methods: {
    selectCard(question) {
      this.selectedQuestion = question;
    },
  },
};
</script>

<style scoped>
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

.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: rgba(0, 0, 0, 0.7);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
}

.enlarged-card {
  transform: scale(1.5);
  transition: transform 0.3s ease;
}

/* Fade transition */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

@media (min-width: 2560px) {
  .cards-grid {
    gap: 50px;
  }

  .enlarged-card {
    transform: scale(2.2);
  }
}
</style>
