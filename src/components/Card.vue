<template>
  <div class="card" @click="clickable && $emit('select', question)">
    <div class="card-content">
      <div
        class="category"
        :style="{ backgroundColor: getCategoryColor(question.category) }"
      >
        {{ question.category }}
      </div>
      <div class="question">{{ question.question }}</div>
      <div class="id">{{ question.id }}</div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    question: {
      type: Object,
      required: true,
    },
    clickable: {
      type: Boolean,
      default: true,
    },
  },
  methods: {
    getCategoryColor(category) {
      const colors = [
        "#ff6b6b",
        "#4ecdc4",
        "#ffe66d",
        "#a8e6cf",
        "#dda0dd",
        "#32cd32",
        "#ffb6c1",
        "#87ceeb",
        "#f0e68c",
        "#ff6347",
      ];
      const categoryColors = JSON.parse(
        localStorage.getItem("categoryColors") || "{}"
      );
      if (!categoryColors[category]) {
        categoryColors[category] =
          colors[Object.keys(categoryColors).length % colors.length];
        localStorage.setItem("categoryColors", JSON.stringify(categoryColors));
      }
      return categoryColors[category];
    },
  },
};
</script>

<style scoped>
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

@media print {
  .card {
    border: 2px dashed #000;
    box-shadow: none;
    transform: none;
  }
  .card:hover {
    transform: none;
  }
}

@media (min-width: 2560px) {
  .card {
    width: 500px;
    height: 550px;
    background-size: 600px 700px;
  }

  .card-content {
    padding: 35px 0;
  }

  .category {
    font-size: 45px;
  }

  .question {
    font-size: 50px;
  }

  .id {
    font-size: 45px;
  }
}
</style>
