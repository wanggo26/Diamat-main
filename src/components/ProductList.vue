<template>
    <div>
      <h2 class="head">Product List</h2><br>
      <div class="product-row">
        <div v-for="(product, index) in products" :key="product.id" :class="{ 'product-card': true, 'last-in-row': (index + 1) % 4 === 0 }">
          <img :src="require(`@/assets/${product.image}`)" class="product-image" alt="Product Image">
          <div class="product-details">
            <h5 class="product-name">{{ product.name }}</h5>
            <p class="product-price">{{ formatCurrency(product.price) }}</p>
            <button class="button" @click="addToCart(product)">Add to Cart</button>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: ['products', 'addToCart'],
    methods: {
      formatCurrency(value) {
        return '₱' + value.toFixed(2);
      },
    },
  };
  </script>
  
  <style>
  .head {
  margin: auto;
  width: 60%;
  border: 3px solid #aa63ec;
  padding: 10px;
  text-align: center;
}

.product-row {
  display: flex;
  flex-wrap: wrap;
  margin: -10px;
}

.product-card {
  flex: 1 0 25%;
  margin: 10px; 
  padding: 10px;
  box-sizing: border-box; 
  border: 1px solid #ccc;
}

.product-image {
  width: 100%; 
  height: 500px; 
  object-fit: contain; 
  display: block; 
}

.product-details {
  text-align: center;
}

.product-name {
  margin-bottom: 5px;
}

.product-price {
  font-weight: bold;
}

.button{
    height: 50px;
    width: 100px;
    background-color: #638eec;
}
.product-name{
    font-size: large;
}
  </style>
  