<template>
    <div>
        <RestoDetail :resto="resto" :addComment="(comment, ratingValue)=> createComment(resto, comment, ratingValue)"/>
        <h2>Restaurants liste</h2>
        <button @click="openRestaurantForm">Ajouter un restaurant</button>
        <RestoForm v-if="openForm" :onValidate="addResto" />
        <ul>
            <li v-for="resto in listResto.length > 0 ? listResto : restaurants" :key="resto.restaurantName" @click=" () => setCurrentResto (resto)"> <!--la boucle va extraire un resto dans la ligne restaurant-->
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
import RestoForm from "./RestoForm";
import {mean, map} from 'lodash'; // du coup on importe seulement mean et map de la bibliothèque


export default {
    components:{
        CommentList,
        Stars,
        RestoDetail,
        RestoForm,
    },
    props: {
        restaurants: [],
        placeApi: {},
        google: {},
        map: {},
    },
    methods: {
        calculateRating(ratings){
            return mean(map(ratings, "stars")); // map va recuperer le champ stars dans chacun des ratings, et en retourner une liste --- mean fait la moyenne de la liste qui est retournée par map
        },
        setCurrentResto (resto) {
            var request = {
                placeId: resto.place_id,
                fields: ['name', 'rating', 'formatted_phone_number', 'geometry', 'review']
            };
            this.placeApi.getDetails(request, (result) => {
                resto.ratings = result.reviews.map((review) => (
                    {
                        stars: review.rating,
                        comment: review.text,
                    }
                ))
                this.resto = resto;
            })
            
        },
        createComment (resto, comment, ratingValue) {
            resto.ratings = [...resto.ratings, {stars:ratingValue, comment}]; // ... est le sprade operator, c a d que ca recupere chaque ligne du tableau et les reinjecte dans le nouveau tableau
        },
        openRestaurantForm() {
            this.openForm = true;
        },
        addResto({nom, rating}) {
            this.listResto.push({
                restaurantName: nom,
                ratings: [],
                rating: rating
            })
            console.info(this.listResto)
        }
    },
    mounted() {
        this.placeApi.nearbySearch({
            location: {lat: -21.124302, lng: 55.7245012},
            radius: 5000,
            type: ['restaurant'],
            },
            (result) => {
                const list = []
                result.forEach(element => {
                    console.log(element)
                    list.push({
                        place_id: element.place_id,
                        restaurantName: element.name,
                        address: element.vicinity,
                        lat: element.geometry.location.lat,
                        long: element.geometry.location.lng,
                        ratings: []
                    })
                    const marker = new this.google.maps.Marker({
                        position: element.geometry.location,
                        map: this.map,
                        title: 'Hello World!'
                    });
                    console.info(marker, this.map)
                });
                this.listResto = list
            }
        )
    },
    data() {
        return {
            resto: null,
            listResto: [],
            openForm: false
        }
    }
}
</script>
