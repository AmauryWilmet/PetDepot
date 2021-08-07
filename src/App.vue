<template>
  <div id="main">
    <Header :lengthCart="cart.length" />
    <div id="container-product" v-for="product in listProducts" :key="product.id">
      <Product :image="product.image" :title="product.title" :description="product.description"
      :price="product.price" :addToCart="addToCart" :isPreview="false" :stars="product.stars" @starClick="starClick"/>
    </div>
    <section id="best-product"> 
      <hr>
      <h3>Best Product</h3>
        <div id="container-product" v-for="bestProduct in listProducts" :key="bestProduct.id">
          <Product v-if="bestProduct.stars > 2" :image="bestProduct.image" :title="bestProduct.title" :description="bestProduct.description"
          :price="bestProduct.price" :addToCart="addToCart" :isPreview="false" />
        </div>
    </section>
    <FormCreatePet :create="createProduct" />
  </div>
</template>

<script>
import Header from './components/Header.vue';
import Product from './components/Product.vue';
import FormCreatePet from './components/FormCreatePet.vue';

import data from './product-data';

export default {
  name: 'App',
  components: {
    Header,
    Product,
    FormCreatePet,
  },
  data() {
    return {
      listProducts: data.listProducts,
      cart: data.cart,
    }
  },
  methods: {
    addToCart() {
      this.cart.push(1);
    },
    
    createProduct(title, description, image, price, visible) {
      let newProduct = {
        "id": 23,
        "title": title, 
        "description": description, 
        "image": image, 
        "price": price,
        "visible": visible,
      };
      console.log(newProduct);
      this.listProducts.push(newProduct)
    },
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#container-product {
  text-align: left;
  padding: 2% 5%;
}
</style>
