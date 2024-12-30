// src/components/RatingDisplay.vue
<template>
  <div class="rating">
    <div class="stars">
      <span v-for="n in 5" :key="n" :class="{ filled: n <= Math.round(rating) }"> ● </span>
    </div>
    <span class="rating-text">{{ rating }}/5</span>
  </div>
</template>

<script>
export default {
  name: 'RatingDisplay',
  props: {
    rating: {
      type: Number,
      required: true,
    },
  },
}
</script>

<style scoped>
.rating {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-bottom: 15px;
}

.stars {
  display: flex;
  gap: 2px;
}

.stars span {
  color: #ddd;
}

.stars span.filled {
  color: gold;
}
</style>
