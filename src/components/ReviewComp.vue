<template>
  <div>
    <div class="review-card" v-for="(review, index) in reviews" :key="index">
      <p>{{ review }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ReviewComp',
  props: {
    reviews: {
      type: Array,
      required: true
    }
  }
}
</script>

<style scoped>
.review-card {
  padding: 15px;
  border: 1px solid #ccc;
  border-radius: 10px;
  margin-top: 10px;
  font-family: 'Mulish', sans-serif;
}
</style>
