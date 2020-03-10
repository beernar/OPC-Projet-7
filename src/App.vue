<template>
  <div id="app">
      <Header />
      <div class="layout">
        <div id="restoExplore">
          <RestoList :restaurants="list.restaurants"/>
        </div>
        <div class="map">
          <Map api-key="AIzaSyC8nyrVz0ip50G0ThC5RoCm9k2uPPCUQ9c"/>
        </div>
      </div>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import RestoList from "./components/RestoList";
import Map from "./components/Map";
import list from "./assets/restos.json"; // import du fichier JSON

export default {
  data: ()=>({
    list,
  }),
  name: 'App',
  components: {
    Header,
    RestoList,
    Map
  }
}
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

.map {
  align-items: flex-end;
  width: 70vw;
}

</style>
