<template>
  <div class="rating-star">
    <span 
      v-for="star in 5" 
      :key="star" 
      :class="{'filled': star <= currentRating}" 
      @click="setRating(star)"
      @mouseover="hoverRating(star)"
      @mouseleave="hoverRating(currentRating)"
    >&#9733;</span>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  name: 'RatingStar',
  emits: ['update:rating'],
  setup(_, { emit }) {
    const currentRating = ref(0);

    const setRating = (rating) => {
      currentRating.value = rating;
      emit('update:rating', rating);
    };

    const hoverRating = (rating) => {
      currentRating.value = rating;
    };

    return {
      currentRating,
      setRating,
      hoverRating
    };
  }
}
</script>

<style scoped>
.rating-star {
  display: flex;
}

.rating-star span {
  font-size: 24px;
  cursor: pointer;
}

.rating-star .filled {
  color: gold;
}
</style>
