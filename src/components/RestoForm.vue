<template>
    <div>
        <input type="text" v-model="nom" />
        <textarea v-model="adresse"></textarea>
        <button @click="validate">Ajouter</button>
    </div>    
</template>

<script>
export default {
    props: {
        inputLat: Number,
        inputLng: Number,
        onValidate: () => {}
    },
    data() {
        return {
            rating: 0,
            nom: "",
            adresse: ""
        }
    },
    methods: {
        validate() {
            this.onValidate({
                nom: this.nom,
                rating: this.rating
            })
        }
    }
}
</script>