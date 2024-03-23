<script setup>
import { ref, onMounted } from 'vue';
import Heading from "./components/Heading.vue"
import Loading from './components/Loading.vue'
import StarRating from './components/StarRating.vue'
import ReviewComments from './components/ReviewComments.vue'


const _isLoading = ref(false);
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
    _isLoading.value = false;
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

    <div v-if="_isLoading">
      <Loading />
    </div>
    <div v-else class="rating-container">
      <StarRating :iconurl="starurl" v-for="(rating, index) in reviewData.ratings" :key="index">
        <template #rating>
          <p>{{ rating }}</p>
        </template>
      </StarRating>
    </div>
  </div>
  <div class="review-container">
    <ReviewComments v-for="{reviewer_name,reviewer_image,status,review} in reviewData.reviews"
      :reviewerimageurl="reviewer_image" :reviewername="reviewer_name" :reviewerstatus="status" :review="review" />
  </div>
</template>
