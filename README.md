The Composition API consists of a number of different Vue.js internals exposed via utility functions. It helps to better organize component code by logical concern and makes it easier to separate component logic from the component template and even reuse that logic across multiple components. Finally, it brings better Typescript support to Vue.js.

What is Composition API or CAPI?
1. Is an alternative to the Option API which is based on Vue 2
2. Defining component internals such as data, methods, and computed props

### Resource on Composition API
https://vuejs.org/guide/extras/composition-api-faq.html#why-composition-api
https://vuejs.org/guide/typescript/overview.html#using-with-composition-api
https://github.com/vuejs/composition-api

# Vue 3 + Vite

This template should help get you started developing with Vue 3 in Vite. The template uses Vue 3 `<script setup>` SFCs, check out the [script setup docs](https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup) to learn more.

## Recommended IDE Setup

- [VS Code](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur) + [TypeScript Vue Plugin (Volar)](https://marketplace.visualstudio.com/items?itemName=Vue.vscode-typescript-vue-plugin).


### Setup Environment

1. Install Node.js

2. Open Terminal,
``` bash
# Run Vite
$ npm init vite

# Install NPM
$ npm install

# Run in development
$ npm run dev

```

### Composition API Setup
https://vuejs.org/api/composition-api-setup.html

### Refs API Docs
https://vuejs.org/api/reactivity-core.html#ref
https://vuejs.org/guide/extras/composition-api-faq.html#reactive-variables-with-ref

### Primitive JavaScript
https://developer.mozilla.org/en-US/docs/Glossary/Primitive

### Reactive Data
https://vuejs.org/api/reactivity-core.html#reactive
### When has an object or an array, which is non-primitive data can use reactive function instead ref function

### Ref VS Reactive
Ref function
- Advantages
1. Works on primitives and non-primitives data

``` bash
# Ref function
const name = ref('The Burger Ramly')
name.value = "Mummy's Burger"

# Reactive function
let name = reactive('The Burger Ramly')
name = "Mummy's Burger"
```

2. Can re-assign the value of the reactive references

``` bash
# Ref function
let posts = ref(['post 1', 'post 2'])
posts.value = ['post 3', 'post 4']

# Reactive function
let posts = reactive(['post 1', 'post 2'])
posts = ['post 3', 'post 4'] // It can mutate any property but cannot replace data itself
```

3. Lend itself to destructuring

``` bash
import usePostComposable from './PostComposable'
export default {
    setup() {
        const { title, author } = usePostComposable()
    }
}

#Ref function
import { ref } from 'vue'
export default() => {
    return {
        title: ref('Awesome'),
        author: ref('Iz'),
        tags: ref(['javascript', 'vue'])
    }
}

```

- Disadvantages
1. Auto unwrapping makes the ref api different depending on context

``` bash
<template>
    {{ name }}
</template>
<script>
import {ref} from 'vue'
export default {
    setup() {
        const name = 'The Ramly Burger'
        console.log(name.value)
        return { name }
    },
    # created() {
    #     console.log(this.name)
    # }
}
</script>
```
2. Having to use .value

Reactive function
- Advantages

1. No need to use .value
2. Consistent interface between, setup, template, and options

``` bash 
<template>
    {{ restaurant.name }}
</template>
<script>
import {reactive} from 'vue'
export default {
    setup() {
        const restaurant = reactive({
            name: 'The Ramly Burger'
        })
        console.log(restaurant.name)
        return { restaurant }
    },
    created() {
        console.log(this.restaurant.name)
    }
}
```

3. Easily made destructurable with toRefs

``` bash
import { reactive, toRefs } from 'vue'
export default() => {
    return toRefs(reactive ({
        title: ref('Awesome'),
        author: ref('Iz'),
        tags: ref(['javascript', 'vue'])
    }))
}
```

- Disadvantages
1. Does not work on primitives values

``` bash
const name = reactive('The Ramly Burger') // Wrong

const restaurant = reactive({
    name: 'The Ramly Burger' // Right
})

Using ref function (string, number, boolean)
Using reactive function (Object)

```

2. Cannot reassign the variable

``` bash

let posts = reactive(['post 1', 'post 2']) 
posts = ['post 3', 'post 4'] // It can mutate any property but cannot replace data itself // Wrong

const restaurant = reactive({
    name: 'The Ramly Burger',
    rating: 5
})
# add
restaurant.address = 'No 3, Walt Street'
# alter
restaurant.name = 'The Pizza Burger'
# delete
delete restaurant.rating // Right

const posts = reactive(['post 1', 'post 2']) 
# update by index
posts[0] = "post 1 updated";
# remove last
posts.pop();
# add new to end
posts.push("post 3") // Right

```

### Watch function
1. In Option API, use this function to keep eye reactive data and execute function whenever that data changes.

### watchEffect function
1. Knows what reactive data we use inside callback function.
2. Don't have access to the old value of data dependency.

### 2 Options to setup attribute
1. Add new script tag like Option API

``` bash
<script>
export default {
    props: {
        name: String,
        price: Number,
    },

    data() {

    },

    methods: {

    }
}
</script>

```

2. Replace in script tag as setup

``` bash
<script setup>
    const props = defineProps({
    name: String,
    price: Number,
})
</script>

```