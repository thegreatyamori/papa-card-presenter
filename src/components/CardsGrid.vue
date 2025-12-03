<template>
  <div class="cards-container">
    <div v-if="questions.length" class="cards-grid">
      <Card v-for="q in questions" :key="q.id" :question="q" />
    </div>
    <NoResults v-if="!questions.length && searched" />
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
</style>
