<script setup>
import { defineEmits, ref } from "vue";

const nameFilter = ref("");

const statusFilter = ref("");

const emit = defineEmits(["applyFilters"]);

const applyFilters = () => {
  emit("applyFilters", {
    name: nameFilter.value,
    status: statusFilter.value,
  });
};
</script>

<template>
  <div class="filters">
    <input type="text" placeholder="Search by name" v-model="nameFilter" />
    <select v-model="statusFilter">
      <option value="">All</option>
      <option value="Alive">Alive</option>
      <option value="Dead">Dead</option>
      <option value="unknown">Unknown</option>
    </select>

    <button @click="applyFilters">Apply Filters</button>
  </div>
</template>

<style scoped>
.filters {
  display: flex;
  justify-content: center;
  margin-bottom: 1rem;
}

.filters input,
.filters select {
  padding: 0.5rem;
  margin-right: 0.5rem;
}

.filters button {
  padding: 0.5rem 1rem;
  background: rgb(39, 43, 51);
  color: white;
  border: none;
  cursor: pointer;
}

.filters button:hover {
  background: rgb(29, 33, 41);
}
</style>
