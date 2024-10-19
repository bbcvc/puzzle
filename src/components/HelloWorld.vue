<script setup lang="ts">
import { ref } from 'vue';
import { html2canvas } from 'html2canvas';
defineProps<{ msg: string }>();

const getAssetsFile = (url: string) => {
  return new URL(`../assets/${url}`, import.meta.url).href;
};
</script>

<template>
  <div class="preview" id="downPoster">
    <img
      v-for="i of Array.from({ length: 3 })"
      :src="getAssetsFile(`小黑2.jpg`)"
      alt=""
    />
  </div>
</template>

<style scoped>
.preview {
  width: 100%;
  aspect-ratio: 5760/3240;
  overflow: hidden;
  background-color: aquamarine;
  display: grid;
  grid-template-columns: repeat(3, 1fr); /* 3列 */
  grid-template-rows: repeat(2, 1fr); /* 2行 */
  gap: 4px;
  background-image: url('../assets/小黑3.jpg');
  background-size: 680px;
  background-repeat: repeat;
  background-position: center;
}
.preview > img {
  width: 100%;
  height: 100%;
  object-fit: contain;
  display: none;
}
</style>
