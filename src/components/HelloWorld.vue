<template>
  <div class="hello">
    <input type="text" v-model="parolaChiave" placeholder="Cerca">
    <div class="bottone_cerca" @click="cercaFilm">Cerca</div>
    <h6 @click="paginaSuccessiva">Prossima</h6>
    <Film v-for="(elemento,index) in filmMostrati" :key="index" :schedaFilm="elemento" class="filmSingolo" /> 
    
  </div>
</template>

<script>
import axios from 'axios'
import Film from './commons/Film.vue'

export default {
  name: 'HelloWorld',
  components: {
    Film,
  },
  data(){
    return{
      ricerca: '',
      parolaChiave : '',
      totaliPagine : "",
      pagina: '0',
      filmMostrati: [],
    }
  },
  methods: {
    paginaSuccessiva(){
      if (this.parolaChiave != '') {
        this.pagina++;
        this.libreriaFilm()
      }
    },
    cercaFilm() {
      this.pagina++
      this.libreriaFilm()
    },
    libreriaFilm(){
        axios.get('https://api.themoviedb.org/3/search/movie', {
          params: {
            api_key: '07f0f906009fb4594eaedc34af8f744d',
            query: this.parolaChiave,
            page: this.pagina,
          }
        })
        .then( (response)=> {
          this.totaliPagine = (response.data.total_pages)
          if (this.pagina <= this.totaliPagine) {
            this.filmMostrati = response.data.results
          }
          console.log(this.filmMostrati);
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
