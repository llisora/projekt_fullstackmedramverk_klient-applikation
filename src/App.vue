<template>
<!--Här valde jag att ta bort Header-komponenten för att kunna dölja headern på vissa undersidor.
Hade kunnat använda v-if men fick det ej att fungera och fick prioritera annat-->
    <RouterView />
</template>

<script>
import { RouterView } from "vue-router";
import Header from "./components/Header.vue";

export default {
  components: {
    Header,
    RouterView,
  },
};
</script>



<style scoped>
main {
  max-width: 1000px;
  width: 100%;
  margin: 0 auto;
}
</style>
