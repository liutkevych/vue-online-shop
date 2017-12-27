<template>
  <div class="cart">
    <h2>Ваш малюнок</h2>
    <p>Зображення: {{ treeName }}</p>
    <p>Рамка: {{ borderName }}</p>
    <p>Відбитки:</p>
    <div class="card" 
    :style="{ backgroundImage: hashUrl, backgroundColor: styleObject.backgroundColor,
     backgroundSize: styleObject.backgroundSize }"></div>
  </div>
</template>

<script>
import {bus} from '../main'

export default {
  name: 'Cart',
  data () {
    return {
      treeName: '',
      borderName: '',
      colors: [],
      sign: '',
      date: '',
      treeObject: {
        backgroundImage: ''
      },
      borderObject: {
        backgroundImage: ''
      },
      styleObject: {
        backgroundColor: '#ffffff',
        backgroundSize: '200px 250px'
      }
    }
  },
  computed: {
    hashUrl: function () {
      return `url("${this.treeObject.backgroundImage}"), url("${this.borderObject.backgroundImage}")`
    }
  },
  created () {
    bus.$on('treeChosen', (data) => {
      this.treeObject.backgroundImage = data.treeUrl
      this.treeName = data.treeName
    })
    bus.$on('borderChosen', (data) => {
      this.borderObject.backgroundImage = data.borderUrl
      this.borderName = data.borderName
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
