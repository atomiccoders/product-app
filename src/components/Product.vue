<template>
  <div class="product">
    <div class="product-image">
      <img :src="image" :alt="`image of ${product.name}`" />
    </div>

    <div class="product-info">
      <h1>{{ title }}</h1>
      <p v-if="inStock > 10">In stock</p>
      <p v-else-if="inStock <= 10 && inStock > 0">Only few left</p>
      <p v-else>Out of stock</p>

      <p>Shipping: {{ shipping }}</p>
      
      <ul>
        <li v-for="(detail, index) in product.details" :key="index">{{ detail }}</li>
      </ul>

      <div class="variants">
        <div v-for="(variant, index) in product.variants"
            :key="variant.variantId"
            class="color-box"
            :style="{ backgroundColor: variant.variantColor }"
            @mouseover="updateProduct(index)">
        </div>
      </div>

      <button @click="addToCart"
              :disabled="!inStock"
              :class="{ 'disabledButton': !inStock }">
        Add to Cart
      </button>

    </div>

    <ProductTabs :reviews="product.reviews" @review-submitted="addReview"/>

  </div>
</template>

<script>
import ProductTabs from './ProductTabs'

export default {
  name: 'Product',
  components: {
    ProductTabs
  },
  props: {
    premium: {
      type: Boolean,
      required: true,
    }
  },
  data() {
    return {
      product: {
        name: 'socks',
        brand: 'vue mastery',
        details: ['80% cotton', '20% polyester', 'Gender-neutral'],
        variants: [
          {
            variantId: 2234,
            variantColor: 'green',
            variantImage: require('../assets/socks-green.jpg'),
            variantQuantity: 11,
          },
          {
            variantId: 2235,
            variantColor: 'blue',
            variantImage: require('../assets/socks-blue.jpg'),
            variantQuantity: 2,
          }
        ],
        reviews: [],
      },
      selectedVariant: 0,
    }
  },
  methods: {
    addToCart () {
      this.$emit('add-to-cart', this.product.variants[this.selectedVariant].variantId);
      this.product.variants[this.selectedVariant].variantQuantity -= 1;
    },
    updateProduct(index) {
      this.selectedVariant = index;
    },
    addReview(productReview) {
      this.product.reviews.push(productReview);
    }
  },
  computed: {
    title() {
      return this.product.brand + ' ' + this.product.name;
    },
    image() {
      return this.product.variants[this.selectedVariant].variantImage;
    },
    inStock() {
      return this.product.variants[this.selectedVariant].variantQuantity;
    },
    shipping() {
      if (this.premium) {
        return 'Free';
      }
      return 2.99;
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  text-transform: capitalize;
}
h3 {
  margin: 40px 0 0;
}
ul {
  /* list-style-type: none; */
  /* padding: 0; */
}
li {
  /* display: inline-block; */
  /* margin: 0 10px; */
}
a {
  color: #42b983;
}
</style>
