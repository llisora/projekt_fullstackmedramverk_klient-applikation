<template>
  <Header />
  <div class="mb-3">
    <h1>Ändra lagersaldo</h1>
    <form
      @submit.prevent="updateProduct(this.$route.params.id)"
      form
      class="form-label"
    >
      <label for="addproduct">Produktnamn:</label>
      <br />
      <input v-model="product.productname" type="text" class="form-control" />
      <br />
      <label for="addproduct">Beskrivning:</label>
      <br />
      <input v-model="product.description" type="text" class="form-control" />
      <br />
      <label for="addproduct">Price:</label>
      <br />
      <input v-model="product.price" type="number" class="form-control" />
      <br />
      <label for="addproduct">Antal:</label>
      <br />
      <input v-model="product.amount" type="number" class="form-control" />
      <br />
      <label for="addproduct">Kategori</label>
      <br />
      <select
        v-model="product.category_id"
        name="category_id"
        id="category_id"
        class="form-control"
      >
        <option value="5">Doftljus</option>
        <option value="6">Vanligt ljus</option>
      </select>
      <br />
      <input type="submit" value="Uppdatera produkt" class="form-control" />
    </form>
    <RouterLink to="/inventory">Tillbaka</RouterLink>
    <div>
      <!--Skriv ut meddelande om lyckad uppdatering-->
      <span> {{ success }}</span>
    </div>
  </div>
</template>

<script>
import Header from "../components/Header.vue";

export default {
  data() {
    //Hämta det ID som skickades med från lager-sidan så att rätt produkt uppdateras
    return {
      id: this.$route.params.id,
      product: [],
      error: "",
      success: "",
    };
  },
  components: {
    Header,
  },
  methods: {
    async getProduct(id) {
      //spara token i variabel
      let token = localStorage.getItem("token");
      //Get anrop för att hämta produkterna
      const resp = await fetch("http://localhost:8000/api/products/" + id, {
        method: "GET",
        headers: {
          Accept: "application/json",
          "Content-type": "application/json",
          //Kolla så man är inloggad
          Authorization: "Bearer " + token,
        },
      });
      const data = await resp.json();
      this.product = data;
    },
    async updateProduct(id) {
      let token = localStorage.getItem("token");

      let productBody = {
        productname: this.product.productname,
        description: this.product.description,
        price: this.product.price,
        amount: this.product.amount,
        category_id: this.product.category_id,
      };
      //PUT-anrop för uppdatering
      const resp = await fetch("http://localhost:8000/api/products/" + id, {
        method: "PUT",
        headers: {
          Accept: "application/json",
          "Content-type": "application/json",
          Authorization: "Bearer " + token,
        },
        body: JSON.stringify(productBody),
      });
      const data = await resp.json();
      //Skriv ut meddelande
      this.success = "Produkt uppdaterad!";
      alert("Produkt uppdaterad!");
    },
  },
  //Ladda in den uppdaterade produkten igen
  mounted() {
    this.getProduct(this.$route.params.id);
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