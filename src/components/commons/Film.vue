<template>
    <div>
        <h4>Titolo: {{schedaFilm.title}}</h4>
        <h5>Titolo Originale: {{schedaFilm.original_title}}</h5>
        <p v-if="schedaFilm.original_language === 'it'">Lingua: &#127470;&#127481;</p>
        <p v-else-if="schedaFilm.original_language === 'en'">Lingua: &#127468;&#127463;</p>
        <p v-else>Lingua: &#127757;</p>
        <span>Voto: {{schedaFilm.vote_average}}</span>
    </div>
</template>

<script>
export default {
    name: 'Film',
    props: {
       schedaFilm: Object,
    }
}
</script>

<style>
h4{
    font-size: 20px;
}

h5{
    font-size: 15px;
}

</style>