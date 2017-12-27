<template>
  <div class="cart">
    <h2>Ваш малюнок</h2>
    <p>Зображення: {{ treeName }}</p>
    <p>Рамка: {{ border }}</p>
    <p>Відбитки:</p>
    <div class="card" :style="treeObject"></div>
  </div>
</template>

<script>
import {bus} from '../main'

export default {
  name: 'Cart',
  data () {
    return {
      treeName: '',
      border: '',
      colors: [],
      sign: '',
      date: '',
      treeObject: {
        backgroundImage: '',
        backgroundColor: '#ffffff',
        backgroundSize: '200px 250px'
      }
    }
  },
  created () {
    bus.$on('treeChosen', (data) => {
      this.treeObject.backgroundImage = `url("${data.treeUrl}")`
      this.treeName = data.treeName
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
