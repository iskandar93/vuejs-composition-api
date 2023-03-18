<template>
    <p>
        <strong>{{ name }}</strong>
        {{ price }}
        <button @click="addToCart">Add To Cart</button>
    </p>
</template>

<script>
export default {

    props: {
        name: String,
        price: Number
    },

    setup(props, { emit }) {
        // console.log(props.name)
        // console.log(props.price)

        const addToCart = () => emit("addToCart", props.name)

        return { addToCart }
    },
}
</script>