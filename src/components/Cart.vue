<template>
  <div class="cart">
    <div class="cart-title"><strong>Ваш малюнок</strong></div>
    <hr>
    <div class="element-description">
      <p><strong>Зображення:</strong> {{ treeName }}</p>
      <p><strong>Рамка:</strong> {{ borderName }}</p>
      <p><strong>Відбитки:</strong></p>
    </div>

    <div class="cart-image" 
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

<style scoped>
  .tree-img {
    width: 100%;
    height: 100%;
  }

  .cart-image {
    width: 200px;
    height: 250px;
    display: inline-block;
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  }

  .cart-title {
    -webkit-margin-before: 1em;
    -webkit-margin-after: 1em;
  }
</style>

