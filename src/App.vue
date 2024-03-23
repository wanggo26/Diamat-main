<template>
  <div id="app" class="app-container">
    <div class="main-content">
      <!-- Pass products and addToCart method as props -->
      <ProductList :products="products" :addToCart="addToCart" />
    </div>
    <div class="sidebar">
      <!-- Pass cart, updateQuantity, and removeFromCart methods as props -->
      <Cart :cart="cart" :updateQuantity="updateQuantity" :removeFromCart="removeFromCart" />
    </div>
  </div>
</template>

<script>
import ProductList from "@/components/ProductList.vue";
import Cart from "@/components/Cart.vue";

export default {
  name: "App",
  data() {
    return {
      products: [
        { id: 1, name: "T-Shirt", price: 100, image: "Shirt.png" },
        { id: 2, name: "Sun Glass", price: 50,  image: "Sunglass.png" },
        { id: 3, name: "Shoes", price: 450,  image: "Shoes.png" },
        { id: 4, name: "Pants", price: 240,  image: "Pants.png" },
        { id: 5, name: "Cap", price: 150,  image: "Cap.png" },
        { id: 6, name: "Handkerchief", price: 25,  image: "Handkerchief.png" },
        { id: 7, name: "Socks", price: 20,  image: "Socks.png" },
        { id: 8, name: "Boxer Shorts", price: 50,  image: "Boxer.png" },
      ],
      cart: [],
    };
  },
  methods: {
    addToCart(product) {
      const cartItem = this.cart.find((item) => item.id === product.id);

      if (cartItem) {
        cartItem.quantity++;
      } else {
        this.cart.push({ ...product, quantity: 1 });
      }
    },
    
    updateQuantity(productId, action) {
      const cartItem = this.cart.find((item) => item.id === productId);

      if (cartItem) {
        if (action === "increase") {
          cartItem.quantity++;
        } else if (action === "decrease" && cartItem.quantity > 1) {
          cartItem.quantity--;
        }
        else if (action === "decrease" && cartItem.quantity == 1) {
          this.cart = this.cart.filter((item) => item.id !== productId);
        }
      }
    },

    removeFromCart(productId) {
      this.cart = this.cart.filter((item) => item.id !== productId);
    },
  },
  components: {
    ProductList,
    Cart,
  },
};
</script>

<style>
.app-container {
  display: flex;
}

.main-content {
  flex: 7;
}

.sidebar {
  flex: 3; 
  background-color: #f0f0f0;
}
</style>
