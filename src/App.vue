<template>
  <div id="app">
    <Header />
    <Map api-key="AIzaSyAQ5VC3npZZR1ULpdFuO7cmpcc2CDeU28g" v-slot="map">
      <div class="layout">
        <div id="restoExplore">
          <RestoList  :placeApi="map.placeApi" :map="map.map" :restaurants="list.restaurants" :google="map.google" />
        </div>
        <div class="map"></div>
      </div>
    </Map>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import RestoList from "./components/RestoList";
import Map from "./components/Map";
import list from "./assets/restos.json"; // import du fichier JSON

export default {
  data: () => ({
    list,
  }),
  name: "App",
  components: {
    Header,
    RestoList,
    Map
  },
  methods: {}
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.layout {
  display: flex;
  justify-content: space-between;
}

.header {
  width: 100%;
  background-color: blueviolet;
}

body {
  margin: 0px;
}
</style>
