<template>
  <div id="app">
    <div class="inputs">
      <inputs @latitude="latInput" @longitude="lngInput" :latitude.sync="latitude" :longitude="longitude" style="float: left;" />
      <worldmap @coordinates="mapClick" :latitude="latitude" :longitude="longitude" style="width: 70%; height: 95%; float: right; z-index: 1"/>
    </div>
  </div>
</template>

<script>

import Inputs from "./components/inputs";
import worldmap from "./components/worldmap";

export default {
  //https://sunrise-sunset.org/api
  //https://vue2-leaflet.netlify.app/quickstart/#accessing-leaflet-api
  //https://apexcharts.com/docs/vue-charts/
  name: 'App',
  data () {
    return {
      latitude: null,
      longitude: null
    };
  },
  components: {
    Inputs,
    worldmap
  },
  methods: {
    latInput(value){
      this.latitude=Number(value);
    },
    lngInput(value){
      this.longitude=Number(value);
    },
    mapClick(value) {
      this.latitude=value[0];
      this.longitude=value[1]
    }
  }
}
</script>

<style>
  html, body {
    margin: 0px !important;
    padding: 0px !important;
    background-color: white;
  }
  #app{
    width: 98%;
    margin: 0 auto;
    display: flex;
    min-height: 100vh;
  }
  .inputs{
    width: 100%;
    padding-top: 26px;
    padding-left: 15px;
  }
</style>
