<!-- 
doit recevoir la props rating et l'afficher
-->
<template>
<div>
    {{ rating.comment }}
    <Stars :value="rating.stars"/>
</div>
    
</template>

<script>
import Stars from "./Stars.vue";
export default {
    components : {
        Stars,
    },
    props: {
        rating: Object,
    },
}
</script>