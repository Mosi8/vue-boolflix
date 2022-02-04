<template>
  <div>
      <span>BOOLFLIX</span>
      <Search class="barracerca" @search="cercaparola"/>
  </div>
</template>

<script>
import Search from '../commons/Search.vue'

export default {
    components: { 
      Search 
    },
    methods: {
        cercaparola: function(ricercaparola) {
            this.$emit('ricercautente',ricercaparola)
        }
    }

}
</script>

<style scoped lang="scss">

div {
    line-height: 60px;
    vertical-align: middle;

    .barracerca {
        float: right;
        margin-right: 20px;
    }

    span{
        margin-left: 20px;
        color: red;
        font-weight: 800;
        font-size: 40px;
        height: 40px;
    }
}

</style>