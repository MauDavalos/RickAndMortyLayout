<template>
  <div class="parent-container">
    <div class="card-container">
      <div class="card" v-for="episode in episodes" :key="episode.id">
        <div>
          <ul class="container">
            <h4><p>Nombre de episodio</p></h4>
            <p>{{episode.name}}</p>
            <h4><b>Fecha de episodio</b></h4>
            <p>{{episode.air_date}}</p>
            <h4><b>Episodio</b></h4>
            <p>{{episode.episode}}</p>

          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: "Episodes",
  data(){
    return{
      characters: null,
      episodes: null
    }
  },
  methods: {
    getDataEpisodes(){
      axios
          .get("https://rickandmortyapi.com/api/episode")
          .then(response=>{
            this.episodes = response.data.results
          })
          .catch(e=>{
            console.log(e)
          })
    }
  },
  mounted(){
    this.getDataEpisodes();
    }
}
</script>

<style scoped>

.card {
  /* Add shadows to create the "card" effect */
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
  transition: 0.3s;
}

/* On mouse-over, add a deeper shadow */
.card:hover {
  box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
}

/* Add some padding inside the card container */
.container {
  padding: 2px 16px;
}

.card-container{
  display: flex;
  justify-content: space-around;
  flex-wrap: wrap;  /* cards 4 columnas */
  max-width: 1000px;

}

.parent-container{
  display: flex;
  justify-content: center;
}
</style>
