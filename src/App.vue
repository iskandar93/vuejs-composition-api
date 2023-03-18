<script>
  export default {

    setup() {
      const name = "The Ramly Burger"

      // function placeOrder() {
      //   alert("Your order has been placed!")
      // }

      const placeOrder = () => alert("Your order has been placed!")

      return { name, placeOrder } // To be access outside setup
    },

  }
</script>

<template>
  <div>
    <h1>{{ name }}</h1>

    <button @click="placeOrder">Place Order</button>

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
