<template>
  <body>
    <div id="app">
      <Main />
    </div>
  </body>
</template>

<script>
import Main from './components/macro/Main.vue'

export default {
  name: 'App',
  components: {
    Main
  }
}
</script>




<style lang="scss">
@import './assets/style/global.scss';

body{
  background-color: rgb(50, 50, 50);
}

</style>
