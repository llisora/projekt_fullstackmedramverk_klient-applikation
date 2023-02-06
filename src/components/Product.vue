<template>
  <article>
    <ul class="list-group">
      <li class="list-group-item">{{ product.productname }}</li>
      <li class="list-group-item">Beskrivning: {{ product.description }}</li>
      <li class="list-group-item">Pris: {{ product.price }}</li>
      <li class="list-group-item">Antal: {{ product.amount }}</li>
      <li class="list-group-item">Kategori: {{ product.category_id }}</li>
    </ul>
    <br>
    <button class="btn btn-danger" @click="$emit('deleteProduct')">
      Radera
    </button>
    <br>
    <router-link :to="{ name: 'Update', params: { id: product.id } }">
      <br>
      <p class="btn btn-primary">Uppdatera</p></router-link>
  </article>
</template>

<script>
export default {
  emits: ["deleteProduct", "updateProduct"],
  props: {
    product: Object,
  },
};
</script>


<style scoped>
article {
  max-width: 800px;
  font-size: 1.2em;
  text-align: center;
  padding: 1em 0;
  background-color: white;
  border: solid 1px #999;
  margin: 1em auto 1em;
  cursor: pointer;
}

article:hover {
  background-color: rgb(153, 153, 153);
}

.table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
}

td,
th {
  border: 1px solid #dddddd;
  text-align: left;
  padding: 8px;
}

tr:nth-child(even) {
  background-color: #dddddd;
}

@media screen and (max-width: 800px) {
  article {
    width: 90%;
  }
}
</style>