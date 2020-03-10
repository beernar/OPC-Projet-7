<template>
    <div style="height: 100%; width: 100%">
        <div class="google-map" ref="googleMap"></div>
        <template v-if="Boolean(this.google) && Boolean(this.map)">
            <slot
                    :google="google"
                    :map="map"
            />
        </template>
    </div>
</template>

<script>
    import GoogleMapsApiLoader from 'google-maps-api-loader'

    export default {
    props: [
        'name',
        'defaultCenter'
    ],

    data() {
        return {
            google: null,
            map: null,
            userCoords: null,
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
                libraries: ['places'],
                apiKey: ""
            });
            this.map = new this.google.maps.Map(this.$refs.googleMap, options)
        }
    }
}
</script>

<style scoped>
    .google-map {
        height: 100vh;
        width: 100vw;
    }
</style>
<!--Fin de l'integration de Googlemap-->