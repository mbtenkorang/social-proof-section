<script setup>
import { ref } from 'vue';

const num = ref(5)
const props = defineProps({
    iconurl: {
        type: String,
        required: true,
    }
})
</script>

<template>
    <div class="rating">
        <div class="stars"><img v-for="i in num" :src="iconurl" alt="" aria-hidden="true" :key="i"></div>
        <slot name="rating" />
    </div>
</template>

