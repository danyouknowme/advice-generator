<template>
  <div id="app">
    <Card />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import Card from "@/components/Card.vue";

@Component({
  components: {
    Card,
  },
})
export default class App extends Vue {}
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  font-family: "Manrope", sans-serif;
  width: 100vw;
  height: 100vh;
  background-color: hsl(218, 23%, 16%);
}
</style>
