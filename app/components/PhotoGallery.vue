<script setup>
import { computed, ref } from "vue";

const photoGallery = ref([]);

const numberOfPhotos = computed(() => {
  return photoGallery.value.length;
});

const evenAlbums = computed(() => {
  return photoGallery.value.filter((item) => item.albumId % 2 === 0);
});

const oddAlbums = computed(() => {
  return photoGallery.value.filter((item) => item.albumId % 2 !== 0);
});

const albumPercentage = computed(() => {
  return evenAlbums.value.length / numberOfPhotos.value;
});

function fetchPhotoGallery() {
  fetch("https://jsonplaceholder.typicode.com/photos")
    .then((response) => response.json())
    .then((json) => {
      photoGallery.value = json;
    });
}
</script>
<template>
  <h1 class="title">Photo Gallery</h1>
  <button @click="fetchPhotoGallery">Fetch Photo Gallery</button>
  <p>
    {{ numberOfPhotos }} photos ({{ evenAlbums.length }} even albums
    {{ oddAlbums.length }} odd albums)
  </p>
  <ul class="photo-gallery-grid">
    <li v-for="photo in photoGallery" :key="`photo-id-${photo.id}`">
      <img :src="photo.thumbnailUrl" />
    </li>
  </ul>
</template>

<style lang="scss">
.photo-gallery-grid {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
}
</style>
