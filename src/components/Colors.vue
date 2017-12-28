<template>
  <div class="colors">
    <div class="element-description">
      <h2>Кольорові відбитки</h2>
      <p>Підберіт найкращі барви, за допомогою ягих ви лишите на малюнку згадку про себе!
      </p>
      <p><strong>Зверніть увагу: при виборі більше двох кольорів збільшується вартість!</strong></p>
      <div class="">
        <ul class="fingers-list">
          <li v-for="(color, index) in colors" class="checkboxFour">
            <input type="checkbox" :value="color.url" :id="color.name" name=""/>
            <label :for="color.name" :style="{ backgroundImage: `url('${color.url}')` }" class="color-lable"></label>
            <!-- <div class="is-centered">
              <img class="finger-image" :src="color.url" alt="">
            </div> -->
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import {bus} from '../main'

export default {
  name: 'Colors',
  data () {
    return {
      colors: [
        {name: 'green', url: './src/assets/BambooLeaves.jpg'},
        {name: 'blue', url: './src/assets/BahamaBlue.jpg'},
        {name: 'darkGreen', url: './src/assets/CottageIvy.jpg'},
        {name: 'purpl', url: './src/assets/LilacPosies.jpg'},
        {name: 'yellow', url: './src/assets/PearTart.jpg'},
        {name: 'terakot', url: './src/assets/PottersClay.jpg'},
        {name: 'red', url: './src/assets/RhubarbStalk.jpg'},
        {name: 'orange', url: './src/assets/Tangelo.jpg'}
      ]
    }
  },
  watch: {
    header: function (newHeader) {
      bus.$emit('newSignTitle', newHeader)
    },
    body: function (newBody) {
      bus.$emit('newSignBody', newBody)
    },
    date: function (newDate) {
      bus.$emit('newSignDate', newDate)
    }
  }
}
</script>

<style scoped>
  .fingers-list {
    list-style-type: none;
    -webkit-padding-start: 0px;
  }

  .finger-image {
    width: 95%;
    height: 95%;
  }

  input[type=checkbox] {
    visibility: hidden;
  }

  .checkboxFour {
    display: inline-block;
    width: 150px;
    height: 150px;
    margin: 20px 20px;
    border-radius: 7px;
    position: relative;
  }

  .checkboxFour label {
    display: block;
    width: 155px;
    height: 155px;
    border-radius: 7px;
    cursor: pointer;
    position: absolute;
    top: 0;
    left: 0;
    z-index: 1;
  }

  .checkboxFour input[type=checkbox]:checked + label {
    border: 3px solid #36c742;
  }

  .color-lable {
    border: 1px solid #9f9999;
    background-size: 100%;
    background-position: center;
  }
</style>
