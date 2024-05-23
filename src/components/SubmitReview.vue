<template>
  <div class="r1">
    <div>
      <p class="rate">Rate & Review Camp</p>
    </div>

    <div class="textArea">
      <textarea 
        v-model="inputText" 
        placeholder="Post your review (240 max characters)" 
        rows="8" 
        cols="50">
      </textarea>
    </div>
    <button @click="submitReview">Submit</button>

    <div class="ratings">
      <div v-for="(heading, index) in headings" :key="index" class="rating">
        <RatingStar :ratingHeading="heading" :selectStars="selectedStars[index]" @update:rating="updateRating(index, $event)" />
      </div>
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
  emits: ['submit-review'],
  setup(props, { emit }) {
    const inputText = ref('');
    const headings = ref(['Service', 'Quality', 'Value', 'Cleanliness']);
    const selectedStars = ref([0, 0, 0, 0]);

    const updateRating = (index, rating) => {
      selectedStars.value[index] = rating;
    };

    const submitReview = () => {
      if (inputText.value.trim() && selectedStars.value.some(rating => rating > 0)) {
        const review = {
          content: inputText.value,
          rating1: selectedStars.value[0],
          rating2: selectedStars.value[1],
          rating3: selectedStars.value[2],
          rating4: selectedStars.value[3],
        };
        emit('submit-review', review);
        inputText.value = '';
        selectedStars.value = [0, 0, 0, 0];
      }
    };

    return {
      inputText,
      headings,
      selectedStars,
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
  box-sizing: border-box;
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
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;
  background-color: #B73C12;
  color: white;
  border: none;
  align-self: flex-start;
}

.ratings {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  margin-top: 20px;
}

.rating {
  flex: 1 1 200px;
  margin-top: 20px;
}
</style>
