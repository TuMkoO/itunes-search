<template>
  <main>
    <form @submit.prevent="searchItunes(searchText)">
      <input
        type="text"
        v-model="searchText"
        placeholder="Input search music..."
      />
      <button type="button" @click="searchItunes(searchText)">Search</button>
      <div v-if="data.results?.length">
        <hr />
        <div v-for="album in data.results" :key="album.artistId">
          <h2>
            Album Name: {{ album.collectionName }} [{{ album.releaseDate }}]
          </h2>
          <h4>Artwork</h4>
          <img :src="album.artworkUrl100" alt="" />
          <h4>Price: {{ album.collectionPrice }}</h4>
        </div>
      </div>
    </form>
  </main>
</template>

<script setup lang="ts">
import { ref } from "vue";
import { itunesSearch } from "./services/iTunesAPI";
import type { ItunesTypes } from "./types/ItunesTypes.interface";

let data = ref<ItunesTypes>({});
let searchText = ref("");
const searchItunes = async (search: string): Promise<void> => {
  const value = await itunesSearch(search);
  data.value = value;
  console.log("data", data.value);
};
</script>

<style>
main {
  width: 100%;
  display: flex;
  align-items: center;
}
form {
  text-align: center;
}
input,
button {
  border: 1px solid #d3d3d3;
  border-radius: 16px;
  height: 44px;
  font-size: 16px;
  outline: none;
  transition: all 0.4s;
  margin: 20px 10px;
  font-weight: 700;
}
input {
  padding: 10px 15px;
}
input:focus {
  border-color: #2978be;
}
button {
  background-color: #fff;
  cursor: pointer;
  color: #2978be;
  padding: 10px 30px;
}
button:hover {
  background-color: #2978be;
  color: #fff;
  border-color: #2978be;
}
hr {
  height: 1px;
  border: none;
  border-top: 1px solid #d3d3d3;
  margin: 5px 0 20px 0;
}
</style>
