<template>
  <header>
    <div class="container">
      <h1>Ljushuset</h1>
      <nav>
        <ul>
          <li><RouterLink to="/">Start</RouterLink></li>
          <li><RouterLink to="/inventory">Lager</RouterLink></li>
          <li><RouterLink to="/login" v-on:click="logout()">Logga ut</RouterLink></li>
        </ul>
      </nav>
    </div>
  </header>
</template>

<script>
import { RouterLink } from "vue-router";
export default {
  components: {
    RouterLink,
  },
  methods: {
    async logout() {
      let token = localStorage.getItem("token");

      const resp = await fetch("http://localhost:8000/api/logout", {
        method: "POST",
        headers: {
          Accept: "application/json",
          "Content-type": "application/json",
          Authorization: "Bearer " + token,
        },
      });
      //Tar bort token vid utloggning
      localStorage.removeItem("token");
      const data = await resp.json();

      //redirect till login-sidan
      this.$router.push("/login");
    },
  },
};
</script>

<style scoped>
header {
  padding: 0.2em;
  background-color: #00034a;
  color: #ffffff;
}

.container {
  display: flex;
  justify-content: space-between;
  max-width: 1000px;
  width: 100%;
  margin: 0 auto;
}

ul {
  display: flex;
  list-style-type: none;
  font-size: 1.1em;
}

li {
  padding: 0 1em;
}

a {
  color: #fff;
  text-decoration: none;
  text-transform: uppercase;
}

a:hover {
  text-decoration: underline;
}

@media screen and (max-width: 1000px) {
  .container {
    width: 95%;
  }
}
</style>