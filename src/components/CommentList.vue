<!--
doit appeler le composant Comment > fait une boucle sur le composant comment
-->
<template>
    <div>
        <h5>Commentaires</h5>
        <!--{{ ratings }}-->
        <ul>
            <li v-for="(rating, index) in ratings" :key="index">
                <Comment :rating="rating"/>
            </li> 
        </ul>
    </div>
</template>


<script>
import Comment from "./Comment.vue";
export default {    
    components:{
        Comment,
    },
    props: {
        ratings: [],// veux dire que mon composant CommentList.vue accepte la propiétée ratings 
    }
}
</script>
