<template>
  <h2>
    Album Name: {{ props.album.collectionName }} [{{ props.album.releaseDate }}]
  </h2>
  <h4>Artwork</h4>
  <img :src="props.album.artworkUrl100" alt="" />
  <h4>Price: {{ props.album.collectionPrice }}</h4>
</template>
<script setup lang="ts">
import type { Result } from "../types/ItunesTypes.interface";

const props = defineProps<{ album: Result }>();
</script>
<style></style>
