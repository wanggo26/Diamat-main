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
        { id: 1, name: "Acer LiquidJade", price: 6799, image: "Acer LiquidJade.png" },
        { id: 2, name: "iphone 15", price: 67000,  image: "iphone 15.png" },
        { id: 3, name: "lenovo k10", price: 4500,  image: "lenovo k10.png" },
        { id: 4, name: "nokia 3310", price: 1999,  image: "nokia 3310.png" },
        { id: 5, name: "oppo a3", price: 3250,  image: "oppo a3.png" },
        { id: 6, name: "realme c1", price: 3200,  image: "realme c1.png" },
        { id: 7, name: "samsung s23", price: 6799,  image: "samsung s23.png" },
        { id: 8, name: "vivo t1", price: 5000,  image: "vivo t1.png" },
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
