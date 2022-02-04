<template>
  <main>
    <!-- <h6 @click="paginaSuccessiva">Prossima</h6> -->
    <div class="container">
      <div class="row justify-content-center">
        <h1 v-if="valorepassato != 0" class="text-center">FILM</h1>
        <Film v-for="(elemento,index) in valorepassato" :key="index" 
        :schedaFilm="elemento"
        class="col-2 contenutiSingolo p-0 m-2"/>
        <div v-if="numpagfilm > 1" class="text-center">
          <span class="tastifrecce" @click="precfilm"><i class="fas fa-arrow-circle-left"></i></span>
          <span class="tastifrecce" @click="succfilm"><i class="fas fa-arrow-circle-right"></i></span>          
        </div>
      </div>
      <div class="row justify-content-center mt-4">
        <h1 v-if="valoreserie != 0" class="text-center">Serie</h1>
        <Serie v-for="elemento in valoreserie" :key="elemento.id" :schedaSerie="elemento" class="col-2 contenutiSingolo p-0 m-2"/> 
        <div v-if="numpagserie > 1" class="text-center">
          <span class="tastifrecce" @click="precserie"><i class="fas fa-arrow-circle-left"></i></span>
          <span class="tastifrecce" @click="succserie"><i class="fas fa-arrow-circle-right"></i></span>
        </div>
      </div>
    </div> 
  </main>
</template>

<script>
import Film from '../commons/Film.vue'
import Serie from '../commons/Serie.vue'

export default {
  name: 'Main',
  components: {
    Film,
    Serie,
  },
  props: {
    valorepassato: Array,
    valoreserie: Array,
    succfilm: Function,
    precfilm: Function,
    succserie: Function,
    precserie: Function,
    numpagserie: Number,
    numpagfilm: Number
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
