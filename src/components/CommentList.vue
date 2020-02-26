<!--
doit appeler le composant Comment > fait une boucle sur le composant comment
v-for in comment
-->
<template>
    <div>
        <h5>Commentaires</h5>
        <ul>
            <li v-for="resto in restaurants" :key="resto.comment">
                <div>{{ resto.comment }}
                    <CommentList :comments="resto.ratings"/> 
                </div>
                </li> 
        </ul>
    </div>
</template>


<!--
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
-->