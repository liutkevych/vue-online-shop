<template>
  <div class="cart">
    <h1>{{ msg }}</h1>
    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Porro nostrum perspiciatis odit nulla quidem libero laborum temporibus ipsum nobis iusto quaerat tempore quae sit fugiat maxime dolore, corporis adipisci assumenda?</p>
    <img v-bind:src="image" class="tree-img">
  </div>
</template>

<script>
import {bus} from '../main'

export default {
  name: 'Cart',
  data () {
    return {
      msg: 'Hello from Cart component',
      description: '',
      border: '',
      colors: [],
      image: '',
      sign: '',
      date: '',
      cost: 0
    }
  },
  created () {
    bus.$on('treeChosen', (data) => {
      this.image = data
    })
  }
}
</script>

<style>

</style>
