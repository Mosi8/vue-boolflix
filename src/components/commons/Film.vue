<template>
    <div>
        <div class="prova">
            <img v-if="schedaFilm.poster_path != null" :src="'https://image.tmdb.org/t/p/w342'+ schedaFilm.poster_path">
            <img v-else :src="'https://montagnolirino.it/wp-content/uploads/2015/12/immagine-non-disponibile.png'">
            <div class="infotitolo">
                <ul>
                    <li><span>Titolo:</span> {{schedaFilm.title}}</li>
                    <li><span>Titolo Originale:</span>  {{schedaFilm.original_title}}</li>
                    <li v-if="schedaFilm.original_language === 'it'"><span>Lingua:</span>  &#127470;&#127481;</li>
                    <li v-else-if="schedaFilm.original_language === 'en'"><span>Lingua:</span>  &#127468;&#127463;</li>
                    <li v-else><span>Lingua:</span>  &#127757;</li>
                    <li><span>Titolo: </span><i class="fas fa-star m-dorato"  v-for="item in Math.ceil(this.schedaFilm.vote_average/2)" :key="item"></i></li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Film',
    props: {
       schedaFilm: Object,
    },
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