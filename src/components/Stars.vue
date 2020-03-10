<!--
Chercher comment integrer des fonts awesome ou vue (étoile)
La font sera un svg vide ou a colorer
-->

<template>
  <div>
    <i class="fas fa-star" :id="star.empty?'empty':'full'" v-for="star in listStars" :key="star.value" @mouseover="()=>changeValue(star.value)"></i> <!--operateur ternaire : si empty est vraie = afficher empty. sinon afficher full-->
  </div>
</template>


<script>
export default {
  props: {
    value: Number,
    max: {
    type:Number,
    default: 5
    },
    onOverStar: Function
  },
  methods : {
    changeValue(value){
      console.log(this);
      this.onOverStar(value)
    }
  },
  computed: {
    listStars() {
        const stars = [];
        for (let i = 0; i<this.max; i++) {
            if (i<this.value) {
                stars.push({
                    value: i+1,
                    empty: false
                })
            } else {
                stars.push({
                    value: i+1,
                    empty: true
                })
            }
        }
        return stars
    }
  }
};
</script>

<style scoped>
#full {
  color: rgb(241, 187, 8);
}

#empty {
  color: rgb(206, 205, 205);
}
</style>