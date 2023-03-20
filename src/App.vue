<script>
  import Meal from './components/Meal.vue';
  import { ref, reactive, watch, watchEffect } from "vue";

  export default {

    components: { Meal },

    setup() {
      //--------------------------------------
      const name = ref("The Ramly Burger")

      const cart = reactive([])
      // const cart = ref([])

      const meal = reactive({ name: 'Hamburger 🍔', price: 5 })

      const meals = reactive([
        { name: 'Hamburger 🍔', price: 5 },
        { name: 'Cheeseburger 🧀', price: 2 },
        { name: 'Hotdog 🌭', price: 10 },
        { name: 'Fries 🍟', price: 20 },
      ])

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
      const addItemToCart = (item) => cart.push(item)
      // const addItemToCart = (item) => cart.value.push(item)

      // Watch reactive object or array will always return a reference to a current value
      // Not right, because when add to cart, the old value should be not appear
      // watch(cart.value, (newValue, oldValue) => console.log(newValue, oldValue)) 

      // // This is good
      // watch(
      //   [name, () => [...cart]], 
      //   (newValue, oldValue) => console.log(newValue, oldValue)
      // ) 

      const removeWatcher = watch([() => [...cart]], (newValue, oldValue) => 
        alert(newValue.join("\n"))
      ) 

      // const removeWatcher = watchEffect(() => alert(cart.join("\n"))) 

      // watch(name, (newName, oldName) => console.log(newName, oldName), {
      //   immediate: true, // The watcher won't wait until the data changes the first time to run and fire immidiately
      //   // deep: true // Allow to watch deeply nested data in object
      // })

      return { name, cart, placeOrder, addItemToCart, meal, meals, removeWatcher} // To be access outside setup
    },

    // watch: {
    //   name(newName, oldName) {
    //     console.log(newName, oldName)
    //   }
    // } Option API

  }
</script>

<template>
  <div>
    <h1>{{ name }}</h1>

    <input type="text" v-model="name" />
    <button @click="placeOrder">Place Order</button>
    <button @click="removeWatcher">Hide Cart Alerts</button>

    <Meal 
      v-for="meal in meals" 
      :name="meal.name" 
      :price="meal.price" 
      @addToCart="addItemToCart" />

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
