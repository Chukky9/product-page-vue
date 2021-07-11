<template>
    <div class="product-display m-3">
            <div class="product-container">
                <div class="product-image">
                    <!--Image goes here-->
                    <img :src="image" alt="table">
                </div>
                <div class="product-info p-4 m-2">
                    <h1>{{title}}</h1>
                    <p v-if="inStock">In Stock</p>
                    <p v-else>Out of Stock</p>
                    <p>Shipping: {{shipping}}</p>
                    <ul>
                        <li v-for="detail in details" :key="detail">{{detail}}</li>
                    </ul>
                    <div v-for="(variant, index) in variants" :key="variant.id" @mouseover="updateVariant(index)" class="color-circle m-1" :style="{backgroundColor: variant.color}"></div>
                    <button class="btn btn-success m-1" @click="addToCart" :disabled="!inStock" :class="{disabledBtn: !inStock}">Add to Cart</button>
                </div>
            </div>
            <review-list :reviews="reviews" v-if="reviews.length"></review-list>
            <review-form @reviewSubmitted="productReview"></review-form>
        </div>
</template>
<script>
import RedTable from '../assets/images/red-table.jpeg';
import YellowTable from '../assets/images/yellow-table.jpeg';
import ReviewForm from './ReviewForm.vue';
import ReviewList from './ReviewList.vue';
export default {
    name: 'ProductItem',
    components: {'review-form': ReviewForm, 'review-list': ReviewList},
    data() {
        return {
            product: 'Tables',
            selectedVariant: 0,
            details: ['Flat 1500x1000 surface top', '2000mm height', 'Smooth Finish', '100% Plastic'],
            variants: [
                {id:1, color:'Red', image: RedTable, quantity: 50},
                {id:2, color:'Yellow', image: YellowTable, quantity: 0}
            ],
            reviews: []
        }
    },
    props: {
        premium: {
            type: Boolean,
            required: true
        }
    },
    methods: {
        addToCart() {
            this.$emit('addToCart', this.variants[this.selectedVariant].id);
        },

        updateVariant(index) {
            this.selectedVariant = index;
        },

        productReview(review) {
            this.reviews.push(review);
        }
    },
    computed: {
        image() {
            return this.variants[this.selectedVariant].image;
        },
        title() {
            return this.product;
        },
        inStock() {
            return this.variants[this.selectedVariant].quantity;
        },
        shipping() {
            if(this.premium) {
                return 'Free';
            }
            return '2.99';
        }
    }
}
</script>
<style scoped>

</style>