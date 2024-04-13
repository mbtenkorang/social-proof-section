<script setup>
import { ref, onMounted } from 'vue';
import Heading from "./components/Heading.vue"
import StarRating from './components/StarRating.vue'
import ReviewComments from './components/ReviewComments.vue'


const reviewData = ref({});
const starurl = ref("/assets/images/icon-star.svg")

const fetchData = async () => {
  try {
    const response = await fetch("./db/data.json");
    if (!response.ok) {
      throw new Error("Network response was not OK")
    }
    const reviews = await response.json();
    reviewData.value = reviews;

  } catch (error) {
    console.warn("Error fetching data:", error)
  }
}

onMounted(() => fetchData())

</script>

<template>
  <div class="header">
    <div class="title-container">
      <Heading />
    </div>

    <div class="rating-container">
      <StarRating :iconurl="starurl" v-for="(rating, index) in reviewData.ratings" :key="index">
        <template #rating>
          <p>{{ rating }}</p>
        </template>
      </StarRating>
    </div>
  </div>

  <div class="review-container">
    <ReviewComments v-for="{id,reviewer_name,reviewer_image,status,review} in reviewData.reviews"
      :reviewerimageurl="reviewer_image" :reviewername="reviewer_name" :reviewerstatus="status" :review="review"
      :key="id" />
  </div>
</template>
