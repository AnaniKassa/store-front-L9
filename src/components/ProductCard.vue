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
            <span class="cart-icon">🛒</span>
            <span class="cart-text"> Add to Cart </span>
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

  display: inline-flex;     
  align-items: center;      
  justify-content: center;  
  gap: 8px;                
  font-size: 16px;
  line-height: 1;           
}

.add-cart-btn:hover {
  background-color: #f4d03f;
}

.cart-icon {
  font-size: 20px;       
  font-weight: bold;
  display: flex;
  align-items: center;
}

</style>
