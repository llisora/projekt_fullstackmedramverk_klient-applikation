<template>
  <div class="mb-3">
    <form @submit.prevent="addProduct()">
      <label for="addproduct" class="form-label">Produktnamn:</label>
      <br />
      <input v-model="productname" type="text" class="form-control" />
      <br />
      <label for="addproduct" class="form-label">Beskrivning:</label>
      <br />
      <input v-model="description" type="text" class="form-control" />
      <br />
      <label for="addproduct" class="form-label">Price:</label>
      <br />
      <input v-model="price" type="number" class="form-control" />
      <br />
      <label for="addproduct" class="form-label">Antal:</label>
      <br />
      <input v-model="amount" type="number" class="form-control" />
      <br />
      <label for="addproduct" class="form-label">Kategori</label>
      <br />
      <select
        v-model="category_id"
        name="category_id"
        id="category_id"
        class="form-select"
      >
        <option value="5">Doftljus</option>
        <option value="6">Vanligt ljus</option>
      </select>
      <br />
      <div class="col-auto">
        <button type="submit" class="btn btn-primary">Lägg till produkt</button>
      </div>
    </form>
    <br />
      <span> {{ success }}</span>
      <span> {{ error }}</span>
  </div>
</template>

<script>
import Header from "../components/Header.vue";

export default {
  data() {
    return {
      //Tömmer värdena
      productname: "",
      description: "",
      price: "",
      amount: "",
      category_id: "",
      success: "",
      error: ""
    };
  },
  components: {
    Header,
  },
  emits: ["productAdded"],
  methods: {
    async addProduct() {
      if (
        //Om dessa fält inte är tomma kör funktionen
        this.productname &&
        this.description &&
        this.price &&
        this.amount &&
        this.category_id != ""
      ) {
        let token = localStorage.getItem("token");

        let productBody = {
          productname: this.productname,
          description: this.description,
          price: this.price,
          amount: this.amount,
          category_id: this.category_id,
        };
        //Post-anrop för att lägga till produkter
        const resp = await fetch("http://localhost:8000/api/products", {
          method: "POST",
          headers: {
            Accept: "application/json",
            "Content-type": "application/json",
            Authorization: "Bearer " + token,
          },
          body: JSON.stringify(productBody),
        });

        const data = await resp.json();

        this.productname = "";
        this.description = "";
        this.price = "";
        this.amount = "";
        this.category_id = "";

        this.$emit("productAdded");
        //Meddelande och alertbox
        this.success = "Produkt tillagd!";
        alert("Produkt tillagd!");
        this.error = "";
      } else {
        //Felmeddelande
        this.error = "Se till att fylla i alla fält!";
      }
    },
  },
};
</script>
<style scoped>
.mb-3 {
  max-width: 80%;
  margin: auto;
}
</style>