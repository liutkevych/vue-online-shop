<template>
  <div class="cart">
    <div class="cart-title">
      <strong>Ваш малюнок</strong>
    </div>
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
      <div class="sign-header sign-font" :style="{ fontFamily: signFont}">{{sign}}</div>
      <div class="sign-body sign-font" :style="{ fontFamily: signFont}">{{signBody}}</div>
      <div class="sign-date sign-font" :style="{ fontFamily: signFont}">{{signDate}}</div>
    </div>

    <div class="cart-footer">
      <button class="btn btn-primary btn-lg" v-on:click="makeOrder">До кошика</button>
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
      signFont: '',
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
  methods: {
    makeOrder: function () {
      let order = {
        treeImage: this.treeObject.backgroundImage,
        treeName: this.treeName
        // You have set ther other data which should send on backend
      }
      console.log(order)
      this.axios.post('http://localhost:3000/api/orders/', order).then((res) => {
        console.log(res.status)
      })
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
    bus.$on('fontChosen', (newFont) => {
      this.signFont = newFont
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
    margin-bottom: 16px;
  }

  .cart-title {
    -webkit-margin-before: 1em;
    -webkit-margin-after: 1em;
  }

  .cart-footer {
    margin-bottom: 16px;
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

