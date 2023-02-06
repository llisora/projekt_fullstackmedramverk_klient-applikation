<template>
  <Header />
  <div class="mb-3">
    <h1>Skapa ny användare</h1>
    <form @submit.prevent="register()" form class="form-label">
      <input
        type="text"
        v-model="name"
        placeholder="Name"
        class="form-control"
      />
      <br />
      <input
        type="text"
        v-model="email"
        placeholder="Email"
        class="form-control"
      />
      <br />
      <input
        type="password"
        v-model="password"
        placeholder="Password"
        class="form-control"
      />
      <br />
      <input type="submit" value="Skapa användare" class="form-control" />
      <br />
      <RouterLink to="/login"> <p class="btn btn-dark">Logga in</p></RouterLink>
      <br>
      <!--Här skrivs felmeddelanden/meddelanden ut-->
      <span> {{ success }}</span>
      <span> {{ error }}</span>
    </form>
  </div>
</template>

<script>
export default {
  data() {
      //Returnera tomma värden
    return {
      name: "",
      email: "",
      password: "",
      error: "",
      succes: "",
    };
  },
  methods: {
    async register() {
        //Om dessa fält ej är tomma kör funktionen
      if (this.name && this.email && this.password != "") {
        let userBody = {
          name: this.name,
          email: this.email,
          password: this.password,
        };
        const resp = await fetch("http://localhost:8000/api/register", {
          method: "POST",
          headers: {
            Accept: "application/json",
            "Content-type": "application/json",
          },
          body: JSON.stringify(userBody),
        });
        const data = await resp.json();
        this.name = "";
        this.email = "";
        this.password = "";

        //Skriv ut meddelanden
        this.success = "Användare skapad!";
        this.error = "";
      } else {
          //Om något fält är tomt - skriv ut detta
        this.error = "Se till att alla fält är ifyllda!";
      }
    },
  },
};
</script>

<style scoped>
.mb-3 {
  max-width: 90%;
  margin: auto;
}

h1 {
  text-align: center;
}
</style>