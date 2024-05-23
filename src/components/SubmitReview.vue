<template>
  <div class="r1">
    <div>
      <p class="rate">Rate & Review Camp</p>
    </div>
    <RatingStar @update:rating="updateRating" class="rating" />
    <div class="textArea">
      <textarea 
        v-model="inputText" 
        placeholder="Post your review (240 max characters)" 
        rows="8" 
        cols="50">
      </textarea>
      <button @click="submitReview">Submit</button>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import RatingStar from './RatingStar.vue';

export default {
  name: 'SubmitReview',
  components: {
    RatingStar
  },
  setup(props, { emit }) {
    const inputText = ref('');
    const currentRating = ref(0);

    const updateRating = (rating) => {
      currentRating.value = rating;
    };

    const submitReview = () => {
      if (inputText.value.trim() && currentRating.value > 0) {
        emit('submit-review', { text: inputText.value, rating: currentRating.value });
        inputText.value = '';  // Clear the textarea after submitting
        currentRating.value = 0; // Reset the rating after submitting
      }
    };

    return {
      inputText,
      currentRating,
      submitReview,
      updateRating
    };
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Mulish:ital,wght@0,200..1000;1,200..1000&display=swap');

.textArea {
  width: 504px;
  height: 160px;
  margin-top: 20px;
}

.textArea textarea {
  width: 100%;
  height: 100%;
  font-family: 'Mulish', sans-serif;
  font-size: 21px;
  font-weight: 200;
  border-radius: 24px;
  box-sizing: border-box; /* Ensures padding and border are included in the element's total width and height */
  padding: 10px;
  background-color: #d9d9d9;
}

.rate {
  font-family: 'Mulish', sans-serif;
  font-size: 28px;
  font-weight: 500;
}

.r1 {
  display: flex;
  flex-direction: column;
}

button {
  margin-top: 10px;
  font-family: 'Mulish', sans-serif;
  font-size: 16px;
  padding: 5px 10px;
  border-radius: 5px;
  cursor: pointer;
}
</style>
