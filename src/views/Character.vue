<template>
  <div class="card-container">
    <div class="card" v-for="character in characters.results" :key="character.id">
      <div>
        <div class="container">
          <h4><b>Nombre</b></h4>
          <p>{{ character.name }}</p>
          <h4><b>Status</b></h4>
          <p>{{ character.status }}</p>
          <h4><b>Imagen</b></h4>
          <img :src="character.image" alt="Avatar" style="width:100%">
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: "Character",
  data() {
    return {
      characters: []
    }
  },
  async created() {
    const firstLoadedData = await axios.get("https://rickandmortyapi.com/api/character");
    this.characters = firstLoadedData.data;
  },
  mounted() {
    this.infiniteScroll();
  },
  methods: {
    infiniteScroll() {
      window.onscroll = () => {
        let bottomOfWindow =
            document.documentElement.scrollTop + window.innerHeight ===
            document.documentElement.offsetHeight;

        if (bottomOfWindow) {
          axios
              .get(this.characters.info.next)
              .then((response) => {
                this.characters.results.push(...response.data.results);
                this.characters.info = response.data.info;
              })
              .catch((error) => console.error(error));
        }
      };
    }
  }
}
</script>

<style scoped>

.card {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  transition: 0.3s;
}

.card:hover {
  box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2);
}

.container {
  padding: 2px 16px;

}

.card-container {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap; /* cards 4 columnas */

}
</style>
