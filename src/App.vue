<template>
  <PCryptoPageVue></PCryptoPageVue>
</template>

<script>
import { defineComponent } from "vue";
import { PCryptoPageVue } from "@/components/pages";

export default defineComponent({
  name: "App",
  components: {
    PCryptoPageVue,
  },
});
</script>

<style>
html,
body {
  width: 100vw;
  height: 100vh;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 100%;
  height: 100%;
  color: white;
  background-color: black;
}
</style>
