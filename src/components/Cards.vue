<template>
  <!-- filters -->
  <Filters @applyFilters="handleApplyFilters" />

  <div class="content-container">
    <Card
      v-for="character in characters"
      :key="character.id"
      :character="character"
    />
  </div>

  <!-- pagination -->
  <Pagination :pageData="pageData" @changePage="handleChangePage" />
</template>

<script setup>
import { ref, onMounted } from "vue";
import Card from "./Card.vue";
import Filters from "./Filters.vue";
import Pagination from "./Pagination.vue";

const characters = ref([]);
const pageData = ref({
  page: 1,
  totalPages: 1,
  next: "https://rickandmortyapi.com/api/character/?page=2",
  prev: null,
});

const handleApplyFilters = (filters) => {
  //  ,change page back to 1
  pageData.value.page = 1;
  fetchCharacters(filters);
};

const handleChangePage = (newPage) => {
  pageData.value.page = newPage;
  fetchCharacters();
};

const constructDynamicQuery = (url, parameters) => {
  if (!parameters || Object.keys(parameters).length === 0) return url;

  const query = Object.keys(parameters)
    .map((key) => key + "=" + parameters[key])
    .join("&");

  //   return url + "?" + query; // if the url doesn't have a query string

  return url + "&" + query; // because the url already has a query string due to the page number
};

const fetchCharacters = async (filters) => {
  try {
    const url = `https://rickandmortyapi.com/api/character/?page=${pageData.value.page}`;
    const query = constructDynamicQuery(url, filters);

    console.log("Fetching characters with query:", query);

    const response = await fetch(query);

    const data = await response.json();
    const charactersData = data.results;

    for (const character of charactersData) {
      if (character.episode.length > 0) {
        const episodeResponse = await fetch(character.episode[0]); // fetch first episode for later iuse in card
        const episodeData = await episodeResponse.json();
        character.firstEpisodeName = episodeData.name; // store episode data in character object
      }
    }

    characters.value = charactersData;

    pageData.value = {
      //   page: will already be changed if page was changed
      ...pageData.value,
      totalPages: data.info.pages,
      next: data.info.next,
      prev: data.info.prev,
    };
    console.log("page data:", pageData.value);
  } catch (error) {
    console.error("Failed to fetch characters or episodes:", error);
  }
};

// fetch characters on component mount
onMounted(fetchCharacters());
</script>

<style scoped>
.content-container {
  display: flex;
  -webkit-box-pack: center;
  justify-content: center;
  -webkit-box-align: center;
  align-items: center;
  flex-wrap: wrap;
  padding: 4.5rem 0px;
  background: rgb(39, 43, 51);
  min-height: calc(-60px + 50vh);
}
</style>
