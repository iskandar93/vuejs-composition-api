<template>
    <p>
        <strong>{{ name }}</strong>
        {{ pricePretty }}
        <!-- <input type="text" v-model="pricePretty" /> -->
        <button @click="addToCart">Add To Cart</button>
    </p>
</template>

<script>
import { computed } from 'vue';

export default {

    props: {
        name: String,
        price: Number
    },

    setup(props, { emit }) {
        // console.log(props.name)
        // console.log(props.price)

        const addToCart = () => emit("addToCart", props.name)
        const pricePretty = computed(() => `$${props.price.toFixed(2)}`)
        // const pricePretty = computed({
            
        //     get() {
        //         return `$${props.price.toFixed(2)}`
        //     },
            
        //     set(price) {
        //         alert(`Sorry, we can not accept ${price}. Nice try!`)
        //     }

        // })

        // const pricePrettySentence = computed(
        //     () => `The price of this item is ${pricePretty.value}`
        // )

        return { addToCart, pricePretty }
    },

    // computed: {
    //     pricePretty() {
    //         return `$${this.price.toFixed(2)}`
    //     }
    // }  // Option API
}
</script>