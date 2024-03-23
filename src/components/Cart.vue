<template>
    <div class="cart-container">
      <h2 class="title">ShoppingCart</h2><hr>
      <ul>
        <li v-for="item in cart" :key="item.id">
          {{ item.name }} - {{ formatCurrency(item.price) }}
                <button class="decrease-button" @click="updateQuantity(item.id, 'decrease')">-</button>
                {{ item .quantity }}
                <button class="increase-button" @click="updateQuantity(item.id, 'increase')">+</button>
                <button class="remove-button" @click="removeFromCart(item.id)">Remove</button>
        </li>
      </ul>
      <br><hr>
      <b><p id="total">Total: {{ formattedTotal }}</p></b>
    </div>
  </template>
  
  <script>
  export default {
    name: 'ShoppingCart',
    props: ['cart', 'updateQuantity', 'removeFromCart'],
    methods: {
      formatCurrency(value) {
        return '₱' + value.toFixed(2);
      },
    },
    computed: {
      formattedTotal() {
        const total = this.cart.reduce((total, item) => total + item.price * item.quantity, 0);
        return this.formatCurrency(total);
      },
    },
  };
  </script>
  
  <style>
    .title{
        text-align: center;
    }
    .cart-container {
    border: 1px solid #ccc;
    padding: 10px;
    }
    .cart-item {
    margin-bottom: 10px;
    }
    .quantity{
        float: right;
    }
    .increase-button{
        margin-left: 15px;
        background-color: rgb(128, 157, 221);
    }
    .decrease-button{
        margin-right: 15px;
        margin-left: 5px;
        background-color: rgb(182, 127, 255);
    }
    .remove-button{
        background-color: rgb(231, 86, 86);
        float: right;
    }
  </style>
  