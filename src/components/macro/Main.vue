<template>
  <main>
    <div class="container">
      <div class="row justify-content-center">
        <h1 v-if="valorepassato != 0" class="text-center col-12">FILM</h1>
        <div v-if="numpagfilm > 1" class="text-center col-4">
          <span class="tastifrecce" @click="precfilm"><i class="fas fa-arrow-circle-left"></i></span>
          <span class="tastifrecce" @click="succfilm"><i class="fas fa-arrow-circle-right"></i></span>          
        </div>
        <div v-if="!caricamentoFilm" class="col-12">
          <div class="row justify-content-center">
            <Film v-for="(elemento,index) in valorepassato" :key="index" 
          :schedaFilm="elemento"
          class="col-2 contenutiSingolo p-0 m-2"/>
          </div>
        </div>
        <Loader v-else class="col-12"/>
      </div>
      <div class="row justify-content-center mt-5">
        <h1 v-if="valoreserie != 0" class="text-center col-12">SERIE</h1>
        <div v-if="numpagserie > 1" class="text-center">
          <span class="tastifrecce" @click="precserie"><i class="fas fa-arrow-circle-left"></i></span>
          <span class="tastifrecce" @click="succserie"><i class="fas fa-arrow-circle-right"></i></span>
        </div>
        <div v-if="!caricamentoSerie" class="col-12">
          <div class="row justify-content-center">
            <Serie v-for="elemento in valoreserie" :key="elemento.id" :schedaSerie="elemento" class="col-2 contenutiSingolo p-0 m-2"/>
          </div>
        </div>
        <Loader v-else class="col-12"/>
      </div>
    </div> 
  </main>
</template>

<script>
import Film from '../commons/Film.vue'
import Loader from '../commons/Loader.vue'
import Serie from '../commons/Serie.vue'

export default {
  name: 'Main',
  components: {
    Film,
    Serie,
    Loader,
  },
  props: {
    valorepassato: Array,
    valoreserie: Array,
    succfilm: Function,
    precfilm: Function,
    succserie: Function,
    precserie: Function,
    numpagserie: Number,
    numpagfilm: Number,
    caricamentoFilm: Boolean,
    caricamentoSerie: Boolean,
  },
}
  

</script>
<style scoped lang="scss">

main {
  position: relative;

  .container {
    padding: 30px 0;
    color: #fff;
    font-weight: bold;

    .tastifrecce {
      font-size: 40px;
      margin: 10px;
      cursor: pointer;
    }
  }

  .contenutiSingolo {
  display: inline-block;
  overflow: hidden;
  }
}
</style>
