<template>
  <div id="app">
    <Home v-if="$store.state.view === VIEW_HOME"/>
    <div v-else>
      <Nav :title="$store.state.view" />
      <!-- FIXME: to avoid vue-quaggajs's infinite event callback, using v-show. -->
      <BarCodeReader v-show="$store.state.view === VIEW_BARCODE_READER" />
      <NutritionFacts v-show="$store.state.view === VIEW_NUTRITION" />
      <NoResults v-show="$store.state.view === VIEW_NOT_FOUND" />
    </div>
  </div>
</template>

<script>
import Home from "./components/Home.vue";
import Nav from "./components/Nav.vue";
import BarCodeReader from "./components/BarCodeReader.vue";
import NutritionFacts from "./components/NutritionFacts.vue";
import NoResults from "./components/NoResults.vue";
import { VIEW_HOME, VIEW_NOT_FOUND, VIEW_BARCODE_READER, VIEW_NUTRITION } from "./store";
import unirest from "unirest";

export default {
  name: "app",
  data: () => ({
    VIEW_HOME,
    VIEW_NOT_FOUND,
    VIEW_BARCODE_READER,
    VIEW_NUTRITION
  }),
  mounted() {
    unirest
      .get("https://toto-vrty-v1.p.rapidapi.com/user/toto-castaldi")
      .header("X-Mashape-Key", "0rNhl0x3XrmshOR4YmmFcBH4CVfMp14NEPmjsn1u6Eklq5nUKW")
      .header("X-Mashape-Host", "toto-vrty-v1.p.rapidapi.com")
      .end(function (result) {
        console.log(result.status, result.headers, result.body);
      });
  },
  components: {
    Home,
    Nav,
    BarCodeReader,
    NutritionFacts,
    NoResults,
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: #fafafa;
}
</style>
