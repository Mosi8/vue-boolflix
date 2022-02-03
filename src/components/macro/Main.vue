<template>
  <main>
    <div class="headerbar">
      <Search class="searchbar" @search="cercaFilm"/>
    </div>
    <!-- <input type="text" v-model="parolaChiave" placeholder="Cerca">
    <button class="bottone_cerca" @click="cercaFilm">Cerca</button> -->
    <h6 @click="paginaSuccessiva">Prossima</h6>
    <div class="container">
      <div class="row justify-content-center">
        <h1 v-if="filmMostrati != 0" class="text-center">FILM</h1>
        <Film v-for="(elemento,index) in filmMostrati" :key="index" :schedaFilm="elemento" class="col-2 contenutiSingolo p-0 m-2"/>
      </div>
      <div class="row justify-content-center">
        <h1 v-if="serieMostrate != 0" class="text-center">Serie</h1>
        <Serie v-for="elemento in serieMostrate" :key="elemento.id" :schedaSerie="elemento" class="col-2 contenutiSingolo p-0 m-2"/> 
      </div>
    </div> 
  </main>
</template>

<script>
import axios from 'axios'
import Film from '../commons/Film.vue'
import Serie from '../commons/Serie.vue'
import Search from '../commons/Search.vue'

export default {
  name: 'Main',
  components: {
    Film,
    Serie,
    Search
  },
  props: {
    valorepassato: String
  },
  data(){
    return{
      parolaChiave : '',
      totaliPagineFilm : "",
      totaliPagineSerie: "",
      paginaFilm: '0',
      paginaSerie: '0',
      filmMostrati: [],
      serieMostrate: [],
    }
  },
  methods: {
    paginaSuccessiva(){
      if ((this.parolaChiave != '')) {
        this.paginaFilm++
        this.paginaSerie++
        this.libreriaFilm()
        this.libreriaSerie()
      }
    },
    cercaFilm(parolaricercata) {
      this.parolaChiave = parolaricercata,
      this.paginaFilm = ''
      this.paginaSerie = ''
      this.paginaFilm++
      this.paginaSerie++
      this.libreriaFilm()
      this.libreriaSerie()
    },
    libreriaFilm(){
        axios.get('https://api.themoviedb.org/3/search/movie', {
          params: {
            api_key: '07f0f906009fb4594eaedc34af8f744d',
            query: this.parolaChiave,
            page: this.paginaFilm,
          }
        })
        .then( (response)=> {
          this.totaliPagineFilm = (response.data.total_pages)
          if (this.paginaFilm <= this.totaliPagineFilm) {
            this.filmMostrati = response.data.results
          }
          console.log(this.filmMostrati);
        })
        .catch(function (error) {
          console.log(error);
        }); 
    },
    libreriaSerie(){
        axios.get('https://api.themoviedb.org/3/search/tv', {
          params: {
            api_key: '07f0f906009fb4594eaedc34af8f744d',
            query: this.parolaChiave,
            page: this.paginaSerie,
          }
        })
        .then( (response)=> {
          this.totaliPagineSerie = (response.data.total_pages)
          if (this.paginaSerie <= this.totaliPagineSerie) {
            this.serieMostrate = response.data.results
          }
          console.log(this.serieMostrate);
        })
        .catch(function (error) {
          console.log(error);
        }); 
    },
  }
}
  

</script>
<style scoped lang="scss">

main {
  position: relative;
  .headerbar {
    z-index: 200;
    background-color: #000;
    height: 60px;
    position: fixed;
    display: block;

    .searchbar {
      height: 40px;
    }
  }

  .container {
    position: relative;
    top: 60px;
    color: #000;
    font-weight: bold;
  }

  .contenutiSingolo {
  display: inline-block;
  overflow: hidden;
  }

  .bottone_cerca {
    display: inline-block;
    background-color: blue;
    color: #fff;
    padding: 5px 20px;
    margin-left: 20px;
    border-radius: 5px;
  }
}
</style>
