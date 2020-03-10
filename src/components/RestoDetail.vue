<template>
    <div v-if="resto" >
        
        <h2>Resto Detail</h2>
        <div>{{ resto.restaurantName }}</div>

            <span>Ajoutez votre commentaire :</span>
            <Stars :onOverStar="changeValue"/>
            <p style="white-space: pre-line;">{{ message }}</p>
            <textarea v-model="message" placeholder="écrivez ici" id="comment"></textarea>
            <button @click="validButton" id="validButton">Validez</button>

    </div>
</template>

<script>
import Stars from "./Stars.vue";
export default {
    components : {
        Stars,
    },
    props : {
        resto : null,
        addComment : ()=> {

        },
    },
    methods : {
        validButton (e) {
            e.preventDefault();
            this.addComment(this.message);
        },
        changeValue(value){
            console.log(value)
        }
    }
}

</script>

<style scoped>
    #validButton {
        height: 5vh;
        width: 5vw;
    }
</style>