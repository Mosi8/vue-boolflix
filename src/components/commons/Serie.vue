<template>
    <div>
        <div class="prova">
            <img v-if="schedaSerie.poster_path != null" :src="'https://image.tmdb.org/t/p/w342'+ schedaSerie.poster_path">
            <img v-else :src="'https://montagnolirino.it/wp-content/uploads/2015/12/immagine-non-disponibile.png'">
            <div class="infotitolo">
                <ul>
                    <li><span>Titolo:</span> {{schedaSerie.name}}</li>
                    <li><span>Overview:</span> {{schedaSerie.overview}}</li>
                    <li v-if="schedaSerie.original_language === 'it'"><span>Lingua:</span>  &#127470;&#127481;</li>
                    <li v-else-if="schedaSerie.original_language === 'en'"><span>Lingua:</span>  &#127468;&#127463;</li>
                    <li v-else><span>Lingua:</span>  &#127757;</li>
                    <li><span>Titolo: </span><i class="fas fa-star m-dorato"  v-for="item in Math.ceil(this.schedaSerie.vote_average/2)" :key="item"></i></li>
                </ul>
            </div>
        </div>
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

<style scoped lang="scss">

.prova {
    position: relative;
    height: 100%;
    width: 100%;

    img {
    height: 100%;
    width: 100%;
    object-position: center;
    }

    .infotitolo {
        height: 100%;
        display: none;
        color: #fff;
        z-index: 200;
        position: absolute;
        top: 0;
        padding: 8px;
        overflow: auto;

        ul {
            list-style-type: none;
            padding: 0;
            margin: 0;
            font-size: 15px;
            font-weight: 400;

            span {
                font-weight: 800;
            }
            .m-dorato {
                color: yellow;
            }
        }
    }
}

.prova:hover img{
    filter: brightness(0.2);
}
.prova:hover .infotitolo{
    display: block;
}

</style>