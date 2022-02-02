<template>
  <div class="hello">
    <input type="text" v-model="parolaChiave" placeholder="Cerca">
    <div class="bottone_cerca" @click="cercaFilm">Cerca</div>
    <h6 @click="paginaSuccessiva">Prossima</h6>
    <Film v-for="(elemento,index) in filmMostrati" :key="index" :schedaFilm="elemento" class="filmSingolo" /> 
    <Serie v-for="elemento in serieMostrate" :key="elemento.id" :schedaSerie="elemento" class="filmSingolo" /> 
  </div>
</template>

<script>
import axios from 'axios'
import Film from './commons/Film.vue'
import Serie from './commons/Serie.vue'

export default {
  name: 'HelloWorld',
  components: {
    Film,
    Serie
  },
  data(){
    return{
      ricerca: '',
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
      if (this.parolaChiave != '') {
        this.paginaFilm++
        this.paginaSerie++
        this.libreriaFilm()
        this.libreriaSerie()
      }
    },
    cercaFilm() {
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

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.filmSingolo {
  width: 600px;
  display: inline-block
  ;
}

.bottone_cerca {
  display: inline-block;
  background-color: blue;
  color: #fff;
  padding: 5px 20px;
  margin-left: 20px;
  border-radius: 5px;
}
</style>
