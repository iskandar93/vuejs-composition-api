<script>
  import Meal from './components/Meal.vue';
  import { ref, reactive } from "vue";

  export default {

    components: { Meal },

    setup() {
      //--------------------------------------
      const name = ref("The Ramly Burger")

      const meal = reactive({ name: 'Hamburger 🍔', price: 5 })
      // console.log(meal.name)
      //Always use .value when accessing or mutating the value
      // name.value = 'Hello from the setup function'

      //--------------------------------------
      // let name = ref("The Ramly Burger")
      // name = 'Hello from the setup function'

      // function placeOrder() {
      //   alert("Your order has been placed!")
      // }

      const placeOrder = () => alert("Your order has been placed!")
      const addItemToCart = (item) => alert(`One ${item} to the cart!`)

      return { name, placeOrder, addItemToCart, meal} // To be access outside setup
    },

  }
</script>

<template>
  <div>
    <h1>{{ name }}</h1>

    <input type="text" v-model="name" />
    <button @click="placeOrder">Place Order</button>

    <Meal :name="meal.name" :price="meal.price" @addToCart="addItemToCart" />

  </div>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
