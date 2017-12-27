<template>
  <div class="cart">
    <div class="cart-title"><strong>Ваш малюнок</strong></div>
    <hr>
    <div class="element-description">
      <p><strong>Зображення:</strong> {{ treeName }}</p>
      <p><strong>Рамка:</strong> {{ borderName }}</p>
      <p><strong>Відбитки: </strong></p>
    </div>

    <div class="cart-image" 
    :style="{ backgroundImage: hashUrl, backgroundColor: styleObject.backgroundColor,
     backgroundSize: styleObject.backgroundSize, backgroundRepeat: styleObject.backgroundRepeat,
     backgroundPosition: styleObject.backgroundPosition}">
      <div class="sign-header sign-font">{{sign}}</div>
      <div class="sign-body sign-font">{{signBody}}</div>
      <div class="sign-date sign-font">{{signDate}}</div>
    </div>
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
      signBody: '',
      signDate: '',
      treeObject: {
        backgroundImage: ''
      },
      borderObject: {
        backgroundImage: ''
      },
      styleObject: {
        backgroundColor: '#ffffff',
        backgroundSize: '60% 60%, 200px 250px',
        backgroundRepeat: 'no-repeat',
        backgroundPosition: 'center'
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
    bus.$on('newSignTitle', (sign) => {
      this.sign = sign
    })
    bus.$on('newSignBody', (newBody) => {
      this.signBody = newBody
    })
    bus.$on('newSignDate', (newDate) => {
      this.signDate = newDate
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

  .sign-header {
    margin-top: 24px;
  }

  .sign-body {
    margin-top: 160px;
  }

  .sign-font {
    font-size: 10px;
  }
</style>

