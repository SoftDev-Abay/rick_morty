<script setup>
import Navbar from "./components/Navbar.vue";
import Header from "./components/Header.vue";
import Cards from "./components/Cards.vue";
</script>

<template>
  <Navbar />
  <Header />
  <Suspense>
    <Cards />
  </Suspense>
</template>

<style scoped>
main {
  padding: 20px;
  font-family: Arial, sans-serif;
  color: #333;
}
</style>
