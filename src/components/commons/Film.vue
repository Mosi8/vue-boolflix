<template>
    <div>
        <div class="prova">
            <img class="poster" v-if="schedaFilm.poster_path != null" :src="'https://image.tmdb.org/t/p/w342'+ schedaFilm.poster_path">
            <img class="poster" v-else :src="'https://montagnolirino.it/wp-content/uploads/2015/12/immagine-non-disponibile.png'">
            <div class="infotitolo">
                <ul>
                    <li><span>Titolo:</span> {{schedaFilm.title}}</li>
                    <li><span>Titolo Originale:</span>  {{schedaFilm.original_title}}</li>
                    <li><span>Lingua: <img :src="require('../../assets/img/flags/'+ schedaFilm.original_language+'.png')"></span></li>
                    <li><span>Voto: </span>
                        <span><i v-for="item in numStelle(schedaFilm.vote_average)" :key="item" class="fas fa-star m-dorato"></i></span>
                        <span><i v-for="item in (5-numStelle(schedaFilm.vote_average))" :key="item" class="far fa-star"></i></span>
                    </li>
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
    methods: {
        numStelle(stelle){
            return Math.ceil(stelle/2)
        }
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
                img {
                    width: 20px;
                }
            }
            .m-dorato {
                color: yellow;
            }
        }
    }
}

.prova:hover .poster{
    filter: brightness(0.2);
}
.prova:hover .infotitolo{
    display: block;
}

</style>