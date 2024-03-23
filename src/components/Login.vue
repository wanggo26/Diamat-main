<template>
    <div>
      <h2>Login</h2>
      <button @click="login">Login</button>
    </div>
  </template>
  
  <script>
  export default {
    methods: {
      login() {
        // Generate a token (dummy token for demonstration)
        const token = 'dummy_token';
  
        // Store the token in local storage
        localStorage.setItem('token', token);
  
        // Redirect to the product list page
        this.$router.push('/products');
      },
    },
  };
  </script>
  
  <style scoped>
  /* Add your styling here if needed */
  </style>
  