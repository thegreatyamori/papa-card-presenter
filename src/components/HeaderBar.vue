<template>
  <header class="header-bar">
    <input
      :value="inputIds"
      @input="$emit('update:inputIds', $event.target.value)"
      placeholder="Ingresa IDs separados por coma (ej: 1,3,5)"
      class="search-input"
      @keydown.enter="$emit('search')"
    />
    <button @click="$emit('search')" class="search-button">Buscar</button>
    <button
      v-if="showViewAll"
      @click="$emit('view-all')"
      class="view-all-button"
    >
      Ver todo
    </button>
    <button v-if="showBack" @click="$emit('back')" class="back-button">
      Volver
    </button>
  </header>
</template>

<script>
export default {
  props: {
    inputIds: {
      type: String,
      default: "",
    },
    showViewAll: {
      type: Boolean,
      default: false,
    },
    showBack: {
      type: Boolean,
      default: false,
    },
  },
  emits: ["update:inputIds", "search", "view-all", "back"],
};
</script>

<style scoped>
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

.view-all-button {
  padding: 15px 20px;
  background: #4ecdc4;
  border: none;
  border-radius: 25px;
  font-family: "Roboto", sans-serif;
  font-size: 16px;
  font-weight: 500;
  color: white;
  cursor: pointer;
  margin-left: 10px;
  transition: background 0.3s;
}

.view-all-button:hover {
  background: #45b7aa;
}

.back-button {
  padding: 15px 20px;
  background: #ff6b6b;
  border: none;
  border-radius: 25px;
  font-family: "Roboto", sans-serif;
  font-size: 16px;
  font-weight: 500;
  color: white;
  cursor: pointer;
  margin-left: 10px;
  transition: background 0.3s;
}

.back-button:hover {
  background: #e55a5a;
}
</style>

<style>
@media print {
  .header-bar {
    display: none;
  }
  .view-all-button,
  .back-button {
    display: none;
  }
}
</style>
