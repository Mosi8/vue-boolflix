<template>
    <div>
        <input type="text" v-model="parolautente" placeholder="Cerca">
        <button class="bottone_cerca" @click="$emit('search', parolautente)">Cerca</button>
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
}
</style>