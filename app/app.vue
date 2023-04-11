<script setup>
import { computed, ref } from "vue";
import TodoViewer from "./components/TodoViewer";
import PhotoGallery from "./components/PhotoGallery";
</script>
<template>
  <div class="container">
    <div class="section">
      <div class="columns">
        <div class="column">
          <PhotoGallery />
        </div>
        <div class="column">
          <TodoViewer title="Test">
            <template v-slot:hero>
              <h2>Subheader</h2>
            </template>
            <template v-slot:metrics="{completed}">
              <h2>{{completed.length}} items completados</h2>
            </template>
          </TodoViewer>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss">
@import "./node_modules/bulma/bulma.sass";
@import "./assets/styles/main.scss";
</style>
