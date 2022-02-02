<template>
    <div>
        <h4>Titolo: {{schedaSerie.name}}</h4>
        <p>{{schedaSerie.overview}}</p>
        <p v-if="schedaSerie.original_language === 'it'">Lingua: &#127470;&#127481;</p>
        <p v-else-if="schedaSerie.original_language === 'en'">Lingua: &#127468;&#127463;</p>
        <p v-else>Lingua: &#127757;</p>
    </div>
</template>

<script>
export default {
    name: 'Serie',
    props: {
       schedaSerie: Object,
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