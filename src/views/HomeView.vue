<template>

  <main class="container text-white mt-4">
    <div class="pt-4 mb-8 relative">
      <input type="text" v-model="searchQuery" @input="getSearchResults" placeholder="Search for a city or state"
        class="w-full bg-transparent border-b focus:border-weather-secondary focus:outline-none">

      <ul class="absolute bg-weather-secondary text-white
                 w-full shadow-md py-2 px-1 top-[50px] ">
        <li v-for="searchResult in mapboxSearchResults" :key="searchResult.id" class="py-2">
          {{ searchResult.place_name }}
        </li>
      </ul>
    </div>

  </main>

</template>

<script setup>
import { ref, computed } from "vue";
import axios from "axios"

const mapboxAPIKey =
  "pk.eyJ1Ijoiam9obmtvbWFybmlja2kiLCJhIjoiY2t5NjFzODZvMHJkaDJ1bWx6OGVieGxreSJ9.IpojdT3U3NENknF6_WhR2Q";
const searchQuery = ref("")
const queryTimeOut = ref(null)
const mapboxSearchResults = ref(null);
const searchError = ref(null);

const getSearchResults = () => {
  clearTimeout(queryTimeOut.value);
  queryTimeOut.value = setTimeout(async () => {
    if (searchQuery.value !== "") {
      try {
        const result = await axios.get(
          `https://api.mapbox.com/geocoding/v5/mapbox.places/${searchQuery.value}.json?access_token=${mapboxAPIKey}&types=place`
        );

        mapboxSearchResults.value = result.data.features;
        console.log("ca marche")
      } catch {
        searchError.value = true;
      }
      return;
    }
    mapboxSearchResults.value = null;
  }, 1000);
};

</script>
