<template>
  <div class="container mx-auto">
    <h1 class="text-2xl my-10 font-bold">Crate Digger</h1>
    <button class="hover:bg-gray-700 rounded-full py-2 px-3 font-semibold hover:text-white bg-gray-400 text-gray-100 mb-20" @click="clearAndRefetch" v-if="albums.length">One Mo'Gin</button>
    <button class="hover:bg-gray-700 rounded-full py-2 px-3 font-semibold hover:text-white bg-gray-400 text-gray-100 mb-20" @click="fetchRandomizedAlbums" v-else>Search Random Albums</button>
    <div class="records flex flex-wrap w-full justify-center">
      <!-- Card 1 -->
      <div class="card-box lg:m-4 shadow-md hover:shadow-lg hover:bg-gray-100 rounded-lg bg-white my-12 flex items-center justify-center flex-col" v-for="album in albums" :key="album.id">
        <!-- Card Image -->
        <img :src="album.cover_medium" alt="album cover" class="overflow-hidden">
        <!-- Card Content -->
        <div class="p-4">
          <h3 class="font-bold text-gray-600 my-2">{{ album.title }}</h3>
          <h4 class="font-medium text-gray-600 my-2">{{ album.artist.name }}</h4>
          <p class="text-justify"></p>
          <div class="mt-5">
            <a href="" class="hover:bg-gray-700 rounded-full py-2 px-3 font-semibold hover:text-white bg-gray-400 text-gray-100">Read More</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
const API_URL = 'https://api.deezer.com/album';

export default {
  name: 'Home',
  data() {
    return {
      albums: [],
      randomNums: [],
    }
  },
  methods: {
    randomizeAlbums() {
      for (let i = 0; i < 10; i++) {
        this.randomNums.push(Math.floor(Math.random() * Math.floor(999999)));
      }
    },
    fetchRandomizedAlbums() {
      this.randomNums = [];
      this.randomizeAlbums();
      this.randomNums.forEach(num => {
        fetch(`${API_URL}/${num}`)
          .then(res => res.json())
          .then(data => {
            console.log(data);
            if (data.id) {
              this.albums.push(data);
            }
          })
          .catch(err => console.error(err));
      });
    },
    clearAndRefetch() {
      this.albums = [];
      this.fetchRandomizedAlbums();
    }
  }
}
</script>

<style scoped>
  .card-box {
    height: fit-content;
  }
</style>