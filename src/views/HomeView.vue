<template>
  <Header />
  <h2>Välkommen till lagerhanteringen för butiken Ljushuset!</h2>
  <p>Klicka på "Lager" i menyn för att hantera lagersaldo.</p>
  <div class="center">
    <RouterLink to="/register">
      <p class="btn btn-primary">Skapa ny användare</p></RouterLink
    >
  </div>
</template>

<script>
import Header from "../components/Header.vue";

export default {
  components: {
    Header,
  },
};
</script>

<style scoped>
h2 {
  text-align: center;
}

p {
  text-align: center;
}
.center {
  text-align: center;
}
</style>
