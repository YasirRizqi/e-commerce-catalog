<template>
  <div id="app" :class="currentTheme">
    <loading-spinner v-if="loading" />
    <product-card v-else :product="product" @next="fetchNextProduct" />
  </div>
</template>

<script>
import ProductCard from './components/ProductCard.vue'
import LoadingSpinner from './components/LoadingSpinner.vue'

export default {
  name: 'App',
  components: {
    ProductCard,
    LoadingSpinner,
  },
  data() {
    return {
      product: {},
      currentIndex: 1,
      loading: false,
      currentTheme: '',
    }
  },
  methods: {
    async fetchProduct(index) {
      this.loading = true
      try {
        const response = await fetch(`https://fakestoreapi.com/products/${index}`)
        const data = await response.json()

        if (data.category === "men's clothing" || data.category === "women's clothing") {
          this.product = data
          this.currentTheme = data.category === "men's clothing" ? 'mens-theme' : 'womens-theme'
        } else {
          this.product = {}
          this.currentTheme = 'unavailable-theme'
        }
      } catch (error) {
        console.error('Error fetching product:', error)
        this.product = {}
        this.currentTheme = 'unavailable-theme'
      }
      this.loading = false
    },
    fetchNextProduct() {
      this.currentIndex = this.currentIndex >= 20 ? 1 : this.currentIndex + 1
      this.fetchProduct(this.currentIndex)
    },
  },
  mounted() {
    this.fetchProduct(this.currentIndex)
  },
}
</script>

<style>
:root {
  --mens-primary: #00205b;
  --mens-secondary: #e8f0ff;
  --womens-primary: #800080;
  --womens-secondary: #ffe6ff;
  --unavailable-primary: #808080;
  --unavailable-secondary: #f5f5f5;
}

#app {
  font-family: Arial, sans-serif;
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  background-color: aliceblue;
}

/* Theme-specific styles */
.mens-theme {
  background-color: var(--mens-secondary);
}

.mens-theme button.buy-now {
  background-color: var(--mens-primary);
  color: white;
}

.mens-theme button.next-product {
  border: 2px solid var(--mens-primary);
  background-color: transparent;
  color: var(--mens-primary);
}

.womens-theme {
  background-color: var(--womens-secondary);
}

.womens-theme button.buy-now {
  background-color: var(--womens-primary);
  color: white;
}

.womens-theme button.next-product {
  border: 2px solid var(--womens-primary);
  background-color: transparent;
  color: var(--womens-primary);
}

.unavailable-theme {
  background-color: var(--unavailable-secondary);
}

.unavailable-theme .next-product-solo {
  border: 2px solid var(--unavailable-primary);
  background-color: transparent;
  color: var(--unavailable-primary);
}
</style>
