
<template>
  <div class="product-card" v-if="product">
    <div class="product-image">
      <img :src="product.image" :alt="product.title" v-if="product.image">
      <unavailable-face v-else />
    </div>
    
    <div class="product-info">
      <h2 class="product-title">{{ product.title || 'This product is unavailable to show' }}</h2>
      <div class="category" v-if="product.category">{{ product.category }}</div>
      
      <rating-display 
        v-if="product.rating" 
        :rating="product.rating.rate" 
      />
      
      <p class="description" v-if="product.description">{{ product.description }}</p>
      
      <div class="price-section" v-if="product.price">
        <span class="price">${{ product.price.toFixed(2) }}</span>
        <div class="buttons">
          <button class="buy-now">Buy now</button>
          <button class="next-product" @click="$emit('next')">Next product</button>
        </div>
      </div>
      <div class="buttons" v-else>
        <button class="next-product-solo" @click="$emit('next')">Next product</button>
      </div>
    </div>
  </div>
</template>

<script>
import RatingDisplay from './RatingDisplay.vue'
import UnavailableFace from './UnavailableFace.vue'

export default {
  name: 'ProductCard',
  components: {
    RatingDisplay,
    UnavailableFace
  },
  props: {
    product: {
      type: Object,
      required: true
    }
  }
}
</script>

<style scoped>
.product-card {
  display: flex;
  gap: 30px;
  padding: 20px;
  border-radius: 8px;
  background: white;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.product-image {
  width: 300px;
  height: 300px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.product-image img {
  max-width: 100%;
  max-height: 100%;
  object-fit: contain;
}

/* ... rest of the styles from previous ProductCard ... */
</style>