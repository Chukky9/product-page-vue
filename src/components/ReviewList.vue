<template>
<div class="review-div p-3">
    <h3>Reviews:</h3>
    <ul>
        <li v-for="(review,index) in reviews" :key="index">
            {{review.name}} gave {{review.rating}} stars.
            <br>
            "{{review.review}}"
        </li>
    </ul>
</div>
    
</template>
<script>
export default {
    name: 'ReviewList',
    props: {
        reviews: {
            type: Array,
            required: true
        }
    }
}
</script>
<style scoped>

</style>