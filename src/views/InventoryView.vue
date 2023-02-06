<template>
  <Header />
  <h2>Lager</h2>
  <!--Hämta funktionen för att lägga till produkt från componenten "addProducts"-->
  <addProducts @productAdded="getProducts()" />
  <Product
    @deleteProduct="deleteProduct(product.id)"
    v-for="product in products"
    :product="product"
    :key="product.id"
  />
</template>

<script>
import Header from "../components/Header.vue";
import Product from "../components/Product.vue";
import addProducts from "../components/addProducts.vue";

export default {
  data() {
    return {
      products: [],
    };
  },
  components: {
    Header,
    Product,
    addProducts,
  },
  methods: {
    async getProducts() {
      let token = localStorage.getItem("token");
    //Get anrop för att skriva ut produkter
      const resp = await fetch("http://localhost:8000/api/products", {
        method: "GET",
        headers: {
          Accept: "application/json",
          "Content-type": "application/json",
          Authorization: "Bearer " + token,
        },
      });

      const data = await resp.json();

      this.products = data;
    },
    async deleteProduct(id) {
      let token = localStorage.getItem("token");
      //Delete-anrop för att radera produkt
      const resp = await fetch("http://localhost:8000/api/products/" + id, {
        method: "DELETE",
        headers: {
          Accept: "application/json",
          "Content-type": "application/json",
          Authorization: "Bearer " + token,
        },
      });
      const data = await resp.json();
      //Alertbox vid raderad produkt
      alert("Produkt raderad!");
      this.getProducts();
    },
  },
  //Ladda in produkter på nytt
  mounted() {
    this.getProducts();
  },
};
</script>


<style scoped>
h2 {
  text-align: center;
  font-size: 2em;
}
</style>