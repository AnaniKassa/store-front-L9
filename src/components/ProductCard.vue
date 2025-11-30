<template>
  <div class="product-card">
    <img :src="product.image" alt="Product Image">
    <router-link :to="`/product/${product.id}`">
      <h2>{{ product.name }}</h2>
    </router-link>
      <p>{{ product.description }}</p>
      <div class="product-details">
        <div class="product-price">
          <p class="price">{{ product.price }}</p>
        </div>
        <div class="product-controls">
          <input type="number" v-model="quantity" min="1" class="quantity-input" />
          <button @click="addToCart" class="add-cart-btn"> 
            <img src="/cart.png" class ="cart-icon"> Add to Cart
          </button>
        </div>
      </div>
    </div>
</template>

<script>
export default {
  name: 'ProductCard',
  props: ['product'],
  data() {
    return {
      quantity: 1
    }
  },
  methods: {
    incrementQuantity() {
      this.quantity++
    },
    decrementQuantity() {
      if (this.quantity > 1) {
        this.quantity--
      }
    },
    addToCart() {
      // Add the product and quantity to the cart
      this.$emit('addToCart', {
        productId: this.product.id,
        quantity: this.quantity
      })
    }
  }
}
</script>

<!-- Add yellow style to button here -->

<style scoped>
.add-cart-btn {
  background-color: #ffc300;
  color: black;
  border: none;
  padding: 10px 15px;
  cursor: pointer;
  font-weight: bold;
  border-radius: 5px;
  display: flex;      
  align-items: center;    
  gap: 8px;             
}

.add-cart-btn:hover {
  background-color: #f4d03f;
}

.cart-icon {
  width: 18px;
  height: 18px;
  display: inline-block;  
  vertical-align: middle;
}
</style>
