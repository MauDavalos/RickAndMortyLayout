<template>
  <div class="card-container">
    <div class="card" v-for="character in characters" :key="character.id">
      <div>
        <div class="container">
          <h4><b>Nombre</b></h4>
          <p>{{character.name}}</p>
          <h4><b>Status</b></h4>
          <p>{{character.status}}</p>
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
  components: {

  },
  data(){
    return{
      characters: null,
      paginations: null,
      currentPage: 1,
      totalPages: null
    }
  },
  methods: {
    getData(){
      axios
          .get("https://rickandmortyapi.com/api/character/?page=2")
      .then(response=>{
        this.characters = response.data.results;
        this.paginations = response.data.info;
        this.totalPages = response.data.info.pages;
      })
      .catch(e=>{
        console.log(e)
      })
    },
    pageChangeHandler(selectedPage) {
      this.currentPage = selectedPage
    }

  },
  mounted(){
    this.getData();
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
  justify-content: space-between;
  flex-wrap: wrap;  /* cards 4 columnas */

}


</style>
