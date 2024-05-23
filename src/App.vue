<template>
  <div class="grid-container">
    <div class="col1">
      <SubmitReview @submit-review="addReview" />
    </div>
    <div class="col2">
      <ReviewComp :reviews="reviews" @delete-review="deleteReview" @toggle-view="toggleView" />
    </div>
      <div>
    
  </div>
  </div>
</template>

<script>
import SubmitReview from "./components/SubmitReview.vue";
import ReviewComp from "./components/ReviewComp.vue";
import myreviews from './db.json'; // Load initial reviews

export default {
  name: 'App',
  components: {
    SubmitReview,
    ReviewComp
  },
  data() {
    return {
      reviews: myreviews
    };
  },
  methods: {
    addReview(review) {
      this.reviews.push(review);
    },
    deleteReview(index) {
      // Remove the review from the array
      this.reviews.splice(index, 1);
    },
    toggleView(index) {
      // Toggle the 'showMore' property of the review
      this.reviews[index].showMore = !this.reviews[index].showMore;
    }
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

.grid-container {
  display: grid;
  grid-template-columns: 1fr 1fr;
}

.col1 {
  padding-right: 20px;
}

.col2 {
  padding-left: 20px;
}
</style>
