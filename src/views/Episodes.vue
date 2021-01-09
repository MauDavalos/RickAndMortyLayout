<template>
  <div class="parent-container">
    <div class="list-container">
      <ul class="styled-list" v-for="episode in episodes.results" :key="episode.id">
        <h4><p>Nombre de episodio</p></h4>
        <li>{{ episode.name }}</li>
        <h4><p>Fecha de episodio</p></h4>
        <li>{{ episode.air_date }}</li>
        <h4><p>Episodio</p></h4>
        <li>{{ episode.episode }}</li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: "Episodes",
  data() {
    return {
      episodes: null
    }
  },
  async created() {
    const firstLoadedData = await axios.get("https://rickandmortyapi.com/api/episode");
    this.episodes = firstLoadedData.data;
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
              .get(this.episodes.info.next)
              .then((response) => {
                this.episodes.results.push(...response.data.results);
                this.episodes.info = response.data.info;
              })
              .catch((error) => console.error(error));
        }
      };
    }
  }
}
</script>

<style scoped>
.parent-container {
  display: flex;
  justify-content: center;
}
.list-container {
  width: 50%;
}
li{
  background-color: #47a1a0;
  padding: 12px 15px;
  color: #ffffff
}
p{
  background-color: #387ca3;
  color: #ffffff;
  padding: 12px 15px;

}
ul{
  margin: 100px;

}
</style>
