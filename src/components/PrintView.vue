<template>
  <div class="print-view">
    <div
      v-for="(group, index) in groupedQuestions"
      :key="index"
      class="print-page"
    >
      <Card v-for="q in group" :key="q.id" :question="q" />
    </div>
  </div>
</template>

<script>
import Card from "./Card.vue";

export default {
  components: {
    Card,
  },
  props: {
    groupedQuestions: {
      type: Array,
      default: () => [],
    },
  },
};
</script>

<style scoped>
.print-view {
  padding: 20px;
  box-sizing: border-box;
  width: 100%;
}

.print-page {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  grid-template-rows: repeat(3, 1fr);
  gap: 5px;
  margin-bottom: 20px;
}

@media print {
  .print-page {
    page-break-after: always;
  }
  .card-content {
    height: 100% !important;
    padding: 3px 0 !important;
  }
  .question {
    font-size: 14px !important;
    margin: 5px 0 !important;
  }
  .category {
    font-size: 10px !important;
  }
  .id {
    font-size: 12px !important;
  }
}
</style>
