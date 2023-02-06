<template>
  <h1>Login</h1>
  <form class="form-label">
    <div class="mb-3">
      <input
        type="text"
        v-model="this.email"
        placeholder="Email"
        class="form-control"
      />
      <br />
      <input
        type="password"
        name="password"
        v-model="this.password"
        placeholder="Password"
        class="form-control"
      />
      <br />
      <!--On click - kör login-metod-->
      <button type="button" v-on:click="login()" class="btn btn-primary">
        Login
      </button>
      <br />
      <!--Felmeddelanden -->
      <span> {{ success }}</span>
      <span> {{ error }}</span>
    </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      success: "",
      error: ""
    };
  },
  methods: {
    async login() {
      //Om email och password ej är tomma kör funktionen
      if (this.email && this.password != "") {
        let loginBody = {
          email: this.email,
          password: this.password,
        };
        //Post-anrop för inloggning
        const resp = await fetch("http://localhost:8000/api/login", {
          method: "POST",
          headers: {
            "Content-type": "application/json",
          },
          body: JSON.stringify(loginBody),
        })
          .then((res) => res.json())
          .then((data) => {
            //Kolla så att token existerar 
            if (data.token == null) {
              //Om token inte existerar - skriv ut detta
              this.error = "Användaren existerar inte";
            } else {
              //Spara till variabel
              let token = data.token;
              //Spara till localstorage
              localStorage.setItem("token", token);
            }
          })
          .catch((err) => (this.error = err));

        this.email = "";
        this.password = "";

        //Redirect till startsidan
        this.$router.push("/");
      } else {
        this.error = "Fyll i användarnamn och lösenord";
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