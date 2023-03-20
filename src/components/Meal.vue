<template>
    <p>
        <strong>{{ name }}</strong>
        <MealPrice :price="price" />
        <!-- <input type="text" v-model="pricePretty" /> -->
        <button @click="addToCart">Add To Cart</button>
    </p>
</template>

<script setup>
const props = defineProps({
    name: String,
    price: Number,
})

const emit = defineEmits(['addToCart'])

import MealPrice from './MealPrice.vue';

const addToCart = () => emit("addToCart", props.name)

// export default {

//     components: { MealPrice }, // Register component

//     props: {
//         name: String,
//         price: Number,
//     },

//     setup(props, { emit }) {
//         // console.log(props.name)
//         // console.log(props.price)

//         const addToCart = () => emit("addToCart", props.name)

//         // const pricePretty = computed({
            
//         //     get() {
//         //         return `$${props.price.toFixed(2)}`
//         //     },
            
//         //     set(price) {
//         //         alert(`Sorry, we can not accept ${price}. Nice try!`)
//         //     }

//         // })

//         // const pricePrettySentence = computed(
//         //     () => `The price of this item is ${pricePretty.value}`
//         // )

//         return { addToCart }
//     },

//     // computed: {
//     //     pricePretty() {
//     //         return `$${this.price.toFixed(2)}`
//     //     }
//     // }  // Option API
// }
</script>

// <script>
// export default {
//     props: {
//         name: String,
//         price: Number,
//     },
// }
// </script>