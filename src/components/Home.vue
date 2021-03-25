<template>
  <div class="homepage">
    <h1>Crate Digger</h1>
    <button @click="fetchRandomizedAlbums">Search Random Albums</button>
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
          })
          .catch(err => console.error(err));
      });
    }
  }
}
</script>

<style lang="scss" scoped>
  .homepage {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
</style>