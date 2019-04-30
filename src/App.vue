<template>
  <div id="app">
    <div class="nav-bar">
      <nav>
        <div class="cart">
          <p>Cart ({{ cart.length }})</p>
        </div>
      </nav>
    </div>
    
    <Product :premium="user.premium" @add-to-cart="updateCart" />

    <footer class="footer"></footer>
  </div>
</template>

<script>
import Product from './components/Product'

export default {
  name: 'app',
  components: {
    Product
  },
  data() {
    return {
      user: {
        premium: true
      },
      cart: [],
    }
  },
  methods: {
    updateCart (id) {
      this.cart.push(id);
    }
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  /* margin-top: 60px; */
}

body {
  margin: 0px;
}

.nav-bar {
  background: linear-gradient(-90deg, #84CF6A, #16C0B0);
  height: 60px;
  margin-bottom: 15px;
}

.product {
  display: flex;
  flex-flow: wrap;
  padding: 1rem;
}

img {
  border: 1px solid #d8d8d8;
  width: 70%;
  margin: 40px;
  box-shadow: 0px .5px 1px #d8d8d8;
}

.product-image {
  width: 80%;
}

.product-image,
.product-info {
  margin-top: 10px;
  width: 50%;
}

.color-box {
  width: 40px;
  height: 40px;
  margin-right: 5px;
  display: inline-block;
}

.cart {
  /* margin-right: 25px; */
  float: right;
  border: 1px solid #d8d8d8;
  background-color: #fff;
  padding: 2px 20px;
}

button {
  margin-top: 10px;
  border: none;
  background-color: #1E95EA;
  color: white;
  height: 40px;
  width: 100px;
  font-size: 14px;
} 

.disabledButton {
  background-color: #d8d8d8;
}

.reviews li .name {
  font-size: small;
  font-weight: 600;
  margin-bottom: 0px;
}

.reviews li .review {
  margin-top: 5px;
}

.reviews li .review span {
  font-weight: 600;
}

.review-form {
  width: 400px;
  padding: 20px;
  margin: 20px 40px;
  border: 1px solid #d8d8d8;
}

input {
  width: 100%;  
  height: 25px;
  margin-bottom: 20px;
}

textarea {
  width: 100%;
  height: 60px;
}

.tab {
  margin-left: 20px;
  cursor: pointer;
}

.activeTab {
  color: #16C0B0;
  text-decoration: underline;
}
</style>
