<script>
  import { defineNuxtComponent } from '#app'
export default defineNuxtComponent ({
  data: () => ({
    photoGallery: []
  }),
  computed: {
    numberOfPhotos() {
      return this.photoGallery.length
    },
    evenAlbums() {
      return this.photoGallery.filter(item => item.albumId % 2 === 0)
    },
    oddAlbums() {
      return this.photoGallery.filter(item => item.albumId % 2 !== 0)
    },
    albumPercentage() {
      return this.evenAlbums.length / this.numberOfPhotos
    }
  },
  methods: {
    fetchPhotoGallery() {
      fetch('https://jsonplaceholder.typicode.com/photos')
      .then(response => response.json())
      .then(json => {this.photoGallery = json})
    }
  }
})
</script>
<template>
    <h1>Photo Gallery</h1>
    <button @click="fetchPhotoGallery">Fetch Photo Gallery</button>
    <p>{{numberOfPhotos}} photos ({{evenAlbums.length}} even albums {{oddAlbums.length}} odd albums)</p>
    <ul v-for="photo in photoGallery" :key="`photo-id-${photo.id}`">
      <li><img :src="photo.thumbnailUrl"/></li>
    </ul>
</template>
