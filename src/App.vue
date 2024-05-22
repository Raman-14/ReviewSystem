<template>
  <div class="grid-container">
    <div class="col1">
    <SubmitReview @submit-review="addReview"/>
    <RatingStar class="rating"/>
  </div>
  <div class="col2">
    <ReviewComp :reviews="reviews"/>
  </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import SubmitReview from "./components/SubmitReview.vue";
import RatingStar from "./components/RatingStar.vue";
import ReviewComp from "./components/ReviewComp.vue";

export default {
  name: 'App',
  components: {
    SubmitReview,
    RatingStar,
    ReviewComp,
  },
  setup() {
    const reviews = ref([]);

    const addReview = (text) => {
      reviews.value.push(text);
    };

    return {
      reviews,
      addReview
    };
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Mulish:ital,wght@0,200..1000;1,200..1000&display=swap');
#app {
  font-family: "Mulish", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin-top: 121px;
}
.rating{
  margin-top:50px;
}

.grid-container {
  display: grid;
  grid-template-columns: 1fr 1fr;
}
</style>
