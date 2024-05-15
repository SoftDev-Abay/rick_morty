<template>
  <article class="characterCard">
    <div class="characterCard-img-wrapper">
      <img v-bind:src="character.image" alt="Garment District Rick" />
    </div>
    <div class="characterCard-ContentWrapper">
      <div class="section">
        <a class="externalLink"
          ><h2>{{ character.name }}</h2></a
        ><span class="status"
          ><span class="status__icon"></span> {{ character.status }} -
          {{ character.species }}</span
        >
      </div>
      <div class="section">
        <span class="text-gray">Last known location:</span
        ><a class="externalLink">{{ character.location.name }}</a>
      </div>
      <div class="section">
        <span class="text-gray">First seen in:</span
        ><a class="externalLink">{{ character.firstEpisodeName }}</a>
      </div>
    </div>
  </article>
</template>

<script setup>
import { defineProps } from "vue";

const props = defineProps({
  character: Object,
});
</script>

<style scoped>
.characterCard {
  width: 600px;
  height: 220px;
  display: flex;
  overflow: hidden;
  background: rgb(60, 62, 68);
  border-radius: 0.5rem;
  margin: 0.75rem;
  box-shadow: rgba(0, 0, 0, 0.1) 0px 4px 6px -1px,
    rgba(0, 0, 0, 0.06) 0px 2px 4px -1px;
}

.characterCard-img-wrapper {
  flex: 2 1 0%;
  width: 100%;
}

.characterCard-img-wrapper img {
  width: 100%;
  height: 100%;
  margin: 0px;
  opacity: 1;
  transition: opacity 0.5s ease 0s;
  object-position: center center;
  object-fit: cover;
}

.characterCard-ContentWrapper {
  flex: 3 1 0%;
  position: relative;
  padding: 0.75rem;
  color: rgb(255, 255, 255);
  display: flex;
  flex-direction: column;
}

.section {
  flex: 1 1 0%;
  display: flex;
  flex-direction: column;
  -webkit-box-pack: center;
  justify-content: center;
}

.externalLink {
  text-decoration: none;
  transition: color 0.2s ease 0s;
  color: rgb(245, 245, 245);
}

.externalLink:hover {
  color: rgb(255, 255, 255);
}

.status {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.status__icon {
  width: 0.75rem;
  height: 0.75rem;
  border-radius: 50%;
  background-color: rgb(255, 0, 0);
}

.text-gray {
  color: rgb(158, 158, 158);
}

span {
  font-size: 16px;
  font-weight: 500;
}

@media (min-width: 768px) {
  .characterCard {
    flex-direction: row;
  }

  .characterCard-img-wrapper {
    width: 200px;
    margin-right: 1rem;
  }
}
</style>
