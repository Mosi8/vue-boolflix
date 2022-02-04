<template>
  <body>
    <div id="app">
      <Header class="headerbar" @ricercautente="cerca"/>
      <Main class="mainpos" :valorepassato="filmMostrati" 
      :valoreserie="serieMostrate" 
      :succfilm="paginaSuccessivaFilm"
      :succserie="paginaSuccessivaSerie"
      :numpagfilm="totaliPagineFilm"
      :numpagserie="totaliPagineSerie"
      :precfilm="paginaPrecedenteFilm"
      :precserie="paginaPrecedenteSerie"
      :stelle="voto"/>
    </div>
  </body>
</template>

<script>
import axios from 'axios'
import Header from './components/macro/Header.vue'
import Main from './components/macro/Main.vue'

export default {
  name: 'App',
  components: {
    Header,
    Main,
  },
  data(){
    return{
      parolaChiave : '',
      totaliPagineFilm : 0,
      totaliPagineSerie: 0,
      paginaFilm: 0,
      paginaSerie: 0,
      filmMostrati: [],
      serieMostrate: [],
      voto: [],
    }
  },
  methods: {
    paginaSuccessivaFilm(){
      if (this.parolaChiave != '') {
        if (this.paginaFilm < this.totaliPagineFilm) {
          this.paginaFilm++
          this.libreriaFilm()
        }
      }
    },
    paginaPrecedenteFilm(){
      if (this.parolaChiave != '') {
        if (this.paginaFilm > 1) {
          this.paginaFilm--
          this.libreriaFilm()
        }
      }
    },
    paginaSuccessivaSerie(){
      if (this.parolaChiave != '') {
        if (this.paginaSerie < this.totaliPagineSerie) {
          this.paginaSerie++
          this.libreriaSerie()
        }
      }
    },
    paginaPrecedenteSerie(){
      if (this.parolaChiave != '') {
        if (this.paginaSerie >1) {
          this.paginaSerie--
          this.libreriaSerie()
        }
      }
    },
    cerca(parola) {
      this.parolaChiave = parola
      this.paginaFilm = 0
      this.paginaSerie = 0
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
          this.voto = (response.data.vote_average)
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




<style lang="scss">
@import './assets/style/global.scss';

body{
  background-color: #000;
  font-family: 'Montserrat', sans-serif;

  .headerbar {
    z-index: 300;
    background-color: rgb(35, 35, 35);
    height: 60px;
    width: 100%;
    position: fixed;
    margin: auto 0;
  }

  .mainpos {
    position: relative;
    top: 60px;
  }
}

</style>
