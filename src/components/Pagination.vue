<template>
  <div class="pagination">
    <button @click="previousPage" :disabled="page <= 1">Previous</button>
    <span>Page {{ page }} of {{ totalPages }}</span>
    <button @click="nextPage" :disabled="page >= totalPages">Next</button>
  </div>
</template>
<script setup>
import { ref, computed, defineProps, defineEmits } from "vue";

const props = defineProps({
  pageData: Object,
});

const emit = defineEmits(["changePage"]);

const page = computed(() => props.pageData.page);
const totalPages = computed(() => props.pageData.totalPages);

const previousPage = () => {
  if (page.value > 1) {
    emit("changePage", page.value - 1);
  }
};

const nextPage = () => {
  if (page.value < totalPages.value) {
    emit("changePage", page.value + 1);
  }
};

console.log("page data from pagination:", props.pageData);
</script>

<style scoped>
.pagination {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 1rem;
}

button {
  padding: 0.5rem 1rem;
  margin: 0 0.5rem;
  border: none;
  border-radius: 0.25rem;
  background: rgb(39, 43, 51);
  color: white;
  cursor: pointer;
}

button:disabled {
  /*  more white */
  background: rgb(124, 129, 138);
  cursor: not-allowed;
}
</style>
