<template>
    <div style="height: 100%; width: 100%">
        <template v-if="Boolean(this.google) && Boolean(this.map)">
            <slot v-if="google && map"
                :google="google"
                :map="map"
                :placeApi="placeApi"
            />
        </template>
        <div class="google-map" ref="googleMap"></div>
    </div>
</template>

<script>
import GoogleMapsApiLoader from 'google-maps-api-loader';
    export default {
    props: [
        'name',
        'defaultCenter',
    ],

    data() {
        return {
            google: null,
            map: null,
            userCoords: null,
            placeApi: null,
            center: {
                lat: 48.842702,
                lng: 2.328434
            }
        }
    },

    async mounted() { //async et await permet d'executer du code asynchrone et d'attendre qu'une fonction asynchrone termine
        await this.initialize() // await permet d'attendre que this.initialize ait fini avant d'executer this.loadUserPosition  
        this.loadUserPosition(); 
    },
    methods: {
        loadUserPosition(){
            if ("geolocation" in navigator) {
                navigator.geolocation.getCurrentPosition((pos) => { // API navigateur >> qui fourni la postion du navigateur de l'internaute
                    let position = {
                        lat: pos.coords.latitude,
                        lng: pos.coords.longitude
                    };
                    console.log(position)
                    this.map.setCenter(position);

                    new this.google.maps.Marker({
                        position: position,
                        map: this.map,
                        icon: '/user.png',
                        title: 'vous'
                    });
                });
            } 
        },
        async initialize() {
            const options = {
                center: this.center,
                zoom: 12,
            };
            this.google = await GoogleMapsApiLoader({
                libraries: ["places"],
                apiKey: "AIzaSyAQ5VC3npZZR1ULpdFuO7cmpcc2CDeU28g"
            });
            this.map = new this.google.maps.Map(this.$refs.googleMap, options)
            this.placeApi = new this.google.maps.places.PlacesService(this.map);

            console.info("place api", this.map);
        }
    }
}
</script>

<style scoped>
    .google-map {
        height: 100vh;
        width: 100vw;
    }

    .map {
    align-items: flex-end;
    width: 70vw;
    }
</style>
<!--Fin de l'integration de Googlemap-->