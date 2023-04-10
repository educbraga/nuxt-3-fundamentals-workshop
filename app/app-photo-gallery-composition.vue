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
  <div>
    <h1>Photo Gallery</h1>
    <button @click="fetchPhotoGallery">Fetch Photo Gallery</button>
    <p>
      {{ numberOfPhotos }} photos ({{ evenAlbums.length }} even albums
      {{ oddAlbums.length }} odd albums)
    </p>
    <ul v-for="photo in photoGallery" :key="`photo-id-${photo.id}`">
      <li><img :src="photo.thumbnailUrl" /></li>
    </ul>
  </div>
</template>
