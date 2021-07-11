<template>
    <form class="review-form" @submit.prevent="onSubmit">
        <h3>Leave a Review</h3>
        <div class="form-group m-1">
            <label for="name">Name:</label>
            <input id="name" type="text" v-model="name" class="form-control"/>
        </div>

        <div class="form-group m-1">
            <label for="review">Review:</label>
            <textarea id="review" v-model="review" class="form-control"></textarea>
        </div>

        <div class="form-group m-1">
            <label for="rating">Kindly leave a rating</label>
            <select id="rating" v-model.number="rating" class="form-control form-control-sm">
                <option>5</option>
                <option>4</option>
                <option>3</option>
                <option>2</option>
                <option>1</option>
            </select>
        </div>

        <input class="btn btn-secondary m-2" type="submit" value="Submit"/>
    </form>
</template>
<script>
export default {
    name: 'ReviewForm',
    data() {
        return {
            name: '',
            review: '',
            rating: null
        }
    },
    methods: {
        onSubmit() {
            if(this.name === '' || this.review === '' || this.rating === null) {
                alert('Please fill out all field.!')
                return
                }

            let productReview = {
                name: this.name,
                review: this.review,
                rating: this.rating
            }
            this.$emit('reviewSubmitted', productReview)

            this.name = ''
            this.review = ''
            this.rating = null
            
        }
    }
}
</script>
<style scoped>

</style>