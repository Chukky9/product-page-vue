<template>
    <div class="container-fluid" id="page">
        <div class="navbar mb-3"></div>
        <div class="cart d-flex justify-content-end align-items-end p-2 m-2"><i class="fas fa-shopping-cart"></i>({{cart.length}})</div>
        <product-item :premium="premium " @addToCart="updateCart"></product-item>
    </div>
</template>
<script>
import ProductItem from './ProductItem.vue';
export default {
    name: 'ProductPage',
    components: {'product-item': ProductItem},
    data() {
        return {
            cart: [],
            premium: false
        }
    },
    methods: {
        updateCart(id) {
            this.cart.push(id);
        }
    },
}
</script>
<style scoped>

</style>