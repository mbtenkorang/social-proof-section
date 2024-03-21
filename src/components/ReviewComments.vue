<script setup>
const props = defineProps({
    reviewerimageurl: {
        type: String,
        required: true
    },
    reviewername: {
        type: String,
        default: "Unknown"
    },
    reviewerstatus: {
        type: String
    },
    review: {
        type: String,
    }
})
</script>


<template>
    <article>
        <div>
            <img :src="reviewerimageurl" :alt="`Photo of ${reviewername}`">
            <div>
                <h3>{{ reviewername }}</h3>
                <p>{{ reviewerstatus }}</p>
            </div>
        </div>
        <p>" {{ review }} "</p>
    </article>
</template>