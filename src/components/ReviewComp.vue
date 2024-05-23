<template>
  <div>
    <div v-for="(review, index) in reviews" :key="index" class="review-card">
      <div class="review-header">

        <div class="profile-info">
          <img src="https://source.unsplash.com/random/200x200?sig=1" alt="Profile Image" class="profile-img" />

          <div class="profile-details">

            <div>
            <p class="profileName">{{review.profile_name}}</p>
            <p>{{review.profile_location}}</p>
            </div>

          </div>
        </div>

        <div class="date">
          <p>{{review.created_at}}</p>
        </div>

      </div>
      <div class="review-content" v-if="review.showMore || !review.showMore">
        <p>{{ review.content }}</p>
      </div>
      <div class="ratings" v-if="review.showMore">
        <p>Service: {{ review.rating1 }}</p>
        <p>Quality: {{ review.rating2 }}</p>
        <p>Value: {{ review.rating3 }}</p>
        <p>Cleanliness: {{ review.rating4 }}</p>
      </div>
      <div class="actions">
      <div>
        <button @click="deleteReview(index)">Delete</button>
      </div>
      <div>
        <button @click="toggleView(index)">{{ review.showMore ? 'Less' : 'More' }}</button>
      </div>
      </div>
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
  },
  methods: {
    deleteReview(index) {
      this.$emit('delete-review', index);
    },
    toggleView(index) {
      this.$emit('toggle-view', index);
    }
  }
}
</script>

<style scoped>
.actions{
  display: flex;
  justify-content: space-between;
}
.review-header{
  display: flex;
  justify-content: space-between;
}
.profileName{
  color: #B73C12;
  font-size: 22.32px;
  font-weight: 800;
}
.review-card {
  padding: 15px;
  border: 1px solid #ccc;
  border-radius: 10px;
  margin-top: 10px;
  font-family: 'Mulish', sans-serif;
}

.profile-info {
  display: flex;
  align-items: center;
}

.profile-img {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  margin-right: 10px;
}

.date {
 
}

.review-content {
  margin-top: 10px;
}

.ratings {
  margin-top: 10px;
}

.actions {
  margin-top: 10px;
}

.actions button {
  margin-right: 10px;
  cursor: pointer;
}
</style>
