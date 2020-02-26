<template>
    <div>
        <h2>Restaurants liste</h2>
        <ul>
            <li v-for="resto in restaurants" :key="resto.restaurantName">
                <div>{{ resto.restaurantName }}
                    <CommentList :comments="resto.ratings"/> 
                </div>
                </li> <!--Données injectées dans le template-->
            <!-- v-for permet de boucler dans restaurants pour recuperer resto à chaque itération, et du coup, afficher tout les resto / v-for est donc une boucle for -->
        </ul>
    </div>
</template>


<script>
import CommentList from "./CommentList.vue";
export default {
    components:{
        CommentList,
    },
    props: {
        restaurants: [],
    }
}
</script>
