<template>

  <main class="container text-white">
    <div class="pt-4 mb-8 relative  items-center my-28   " @z-modal="closeme">
      <input type="text" 
      v-model="searchQuery"
      @input="getSearchResults"
      placeholder="Search for a city or state"
        class="  py-6 px-5 text-3xl w-full bg-transparent border-b focus:border-weather-secondary focus:outline-none focus:shadow-[0px_1px_0_0_#004E71] placeholder-white items-center mx-auto my-auto -z-0 "
        
      />
     <ul
        class="absolute  bg-purple-700 text-white w-full shadow-md py-2 my-10 px-1 top-[66px] bg-opacity-50"
        v-if="mapboxSearchResults"
      >
        <p class="py-2" v-if="searchError">
          Sorry, something went wrong, please try again.
        </p>
        <p
          class="py-2"
          v-if="!searchError && mapboxSearchResults.length === 0"
        >
          No results match your query, try a different term.
        </p>
        <template v-else>
          <li
            v-for="searchResult in mapboxSearchResults"
            :key="searchResult.id"
            class="py-4  cursor-pointer capitaliz border-b-2 "
            @click="previewCity(searchResult)"
          >
            {{ searchResult.place_name }}
          </li>
        </template>
      </ul>
    </div>
    <div class="flex flex-col gap-4">
      
    </div>
    
  </main>
  
</template>

<script setup> 


import axios from 'axios';
import { useRoute, useRouter } from 'vue-router';
import { ref } from 'vue';
const queryTimeout = ref(null);
const mapboxAPIKey =
  "pk.eyJ1Ijoiam9obmtvbWFybmlja2kiLCJhIjoiY2t5NjFzODZvMHJkaDJ1bWx6OGVieGxreSJ9.IpojdT3U3NENknF6_WhR2Q";
const mapboxSearchResults = ref(null);
const searchError = ref(null);

const searchQuery = ref('')
const getSearchResults = () => {
  clearTimeout(queryTimeout.value);
  queryTimeout.value = setTimeout(async () => {
    if (searchQuery.value !== "") {
      try {
        const result = await axios.get(
          `https://api.mapbox.com/geocoding/v5/mapbox.places/${searchQuery.value}.json?access_token=${mapboxAPIKey}&types=place`
        );
        mapboxSearchResults.value = result.data.features;
        
      } catch {
        searchError.value = true;
      }

      return;
    }
    mapboxSearchResults.value = null;
  }, 300);
};

const router = useRouter ();

const previewCity = (searchResult)=>{

const [city,state] = searchResult.place_name.split(',')
router.push({
    name:"cityView",
     params: { state: state.replaceAll(" ", ""), city: city },
     query: {
      lat: searchResult.geometry.coordinates[1],
      lng: searchResult.geometry.coordinates[0],
      preview: true,
    },
})
}
  



</script>

<style>

</style>