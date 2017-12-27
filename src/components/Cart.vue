<template>
  <div class="cart">
    <h2>Ваш малюнок</h2>
    <p>Зображення: {{ description }}</p>
    <p>Рамка:</p>
    <p>Відбитки:</p>
    <div class="card"><img v-bind:src="image" class="tree-img"></div>
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
      this.image = data.treeUrl
      this.description = data.treeName
      console.log(data)
    })
  }
}
</script>

<style>
.tree-img {
  width: 100%;
  height: 100%;
}
</style>
