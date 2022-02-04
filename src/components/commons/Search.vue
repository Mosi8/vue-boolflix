<template>
    <div>
        <input type="text" v-model="parolautente" @keyup.enter="$emit('search', parolautente)" placeholder="Cerca un fim o una serie">
        <div class="bottone_cerca p-0" @click="$emit('search', parolautente)"><i class="fas fa-search"></i></div>
    </div>
</template>

<script>
export default {
    name: 'Search',
    data(){
        return {
            parolautente: '',
        }
    }
}
</script>

<style scoped lang="scss">

div {
    height: 100%;
    line-height: 60px;
    vertical-align: middle;
    position: relative;
    display: inline-block;

    input {
        height: 40px;
        width: 300px;
        line-height: 40px;
        border-radius: 20px 20px;
        border: solid 1px #fff;
        padding: 0 20px;
    }

    .bottone_cerca {
        display: inline-block;
        font-size: 20px;
        line-height: 40px;
        color: rgb(100, 100, 100);
        cursor: pointer;
        position: absolute;
        right: 10px;
        top: 20px;
        transform: translateY(-18%);
  }
}
</style>