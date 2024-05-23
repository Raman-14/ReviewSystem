<template>
  <div class="rating-star">
    <span>{{ ratingHeading }}</span>
    <span 
      v-for="star in totalStar" 
      :key="star" 
      :class="{ 'filled': star <= hoverRating || (hoverRating === 0 && star <= currentRating) }"
      @click="setRating(star)"
      @mouseover="setHoverRating(star)"
      @mouseleave="setHoverRating(0)"
    >&#9733;</span>
  </div>
</template>

<script>
import { ref, watch, onMounted } from 'vue';

export default {
  name: 'RatingStar',
  emits: ['update:rating'],
  props: {
    ratingHeading: {
      type: String,
      required: true
    },
    selectStars: {
      type: Number,
      required: true
    }
  },
  setup(props, { emit }) {
    const currentRating = ref(props.selectStars);
    const hoverRating = ref(0);
    const totalStar = 5;

    onMounted(() => {
      currentRating.value = props.selectStars;
    });

    watch(() => props.selectStars, (newRating) => {
      currentRating.value = newRating;
    });

    const setRating = (rating) => {
      currentRating.value = rating;
      emit('update:rating', rating);
    };

    const setHoverRating = (rating) => {
      hoverRating.value = rating;
    };

    return {
      currentRating,
      hoverRating,
      setRating,
      setHoverRating,
      totalStar
    };
  }
}
</script>

<style scoped>
.rating-star {
  display: flex;
  align-items: center;
}

.rating-star span {
  font-size: 24px;
  cursor: pointer;
}

.rating-star .filled {
  color: gold;
}
</style>
