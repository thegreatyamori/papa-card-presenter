<template>
  <p class="no-results">No se encontraron preguntas</p>
</template>

<script>
export default {};
</script>

<style scoped>
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

@media (min-width: 2560px) {
  .no-results {
    font-size: 120px;
    padding: 70px;
  }
}
</style>
