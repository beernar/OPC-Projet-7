<template>
    <div>
        <RestoDetail :resto="resto" :addComment = "(comment)=> createComment(resto, comment)"/>
        <h2>Restaurants liste</h2>
        <ul>
            <li v-for="resto in restaurants" :key="resto.restaurantName" @click=" () => setCurrentResto (resto)"> <!--la boucle va extraire un resto dans la ligne restaurant-->
                <div>{{ resto.restaurantName }}
                    <Stars :value = "calculateRating(resto.ratings)"></Stars> <!--je vais chercher les ratings dans le resto actuel-->
                    <CommentList :ratings="resto.ratings"/> <!--:ratings veux dire v-bind ratings, veux dire que j'attribut les props de ratings à CommentList-->
                </div>
                </li> <!--Données injectées dans le template-->
            <!-- v-for permet de boucler dans restaurants pour recuperer resto à chaque itération, et du coup, afficher tout les resto / v-for est donc une boucle for -->
        </ul>
    </div>
</template>


<script>
import CommentList from "./CommentList.vue";
import Stars from "./Stars.vue";
import RestoDetail from "./RestoDetail";
import {mean, map} from 'lodash'; // du coup on importe seulement mean et map de la bibliothèque
export default {
    components:{
        CommentList,
        Stars,
        RestoDetail,
    },
    props: {
        restaurants: [],
    },
    methods: {
        calculateRating(ratings){
            return mean(map(ratings, "stars")); // map va recuperer le champ stars dans chacun des ratings, et en retourner une liste --- mean fait la moyenne de la liste qui est retournée par map
        },
        setCurrentResto (resto) {
            this.resto = resto;
        },
        createComment (resto, comment) {
            resto.ratings = [...resto.ratings, {stars:4, comment}]; // ... est le sprade operator, c a d que ca recupere chaque ligne du tableau et les reinjecte dans le nouveau tableau
        },
    },
    data() {
        return {
            resto: null,
        }
    }
}
</script>
