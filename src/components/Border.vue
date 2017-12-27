<template>
  <div class="boder">
    <div class="element-description">
      <h2>Рамка</h2>
      <p>Підберіть рамку, яка пасуватиме вашій урочистості та допвнить інтерєр, адже ви не просто лишете на ній вілбитки пальців, а створите предмет декору для офісу чи оселі.</p>
    </div>
    <ul class="border-list">
      <li v-for="(border, index) in borders" class="card border">
        <div class="is-centered">
          <img :src="border.url" v-on:click="addBorder(index)" class="border-img">
        </div>
      </li>
    </ul>
  </div>
</template>

<script>

import {bus} from '../main'

export default {
  name: 'Border',
  data () {
    return {
      borders: [{
        id: 1,
        name: 'New border',
        url: 'http://www.uvassociates.in/sites/default/files/images/borders/Red-yellow-flowery-petals-ceramic-rectangular-powerpoint-border.png',
        cost: 25
      }, {
        id: 2,
        name: 'New border 2',
        url: 'https://cdn.pixabay.com/photo/2015/12/20/20/19/picture-frame-1101626_1280.png',
        cost: 30
      }, {
        id: 3,
        name: 'New border 3',
        url: 'https://cdn.pixabay.com/photo/2017/07/20/19/56/art-2523530_1280.png',
        cost: 25
      }, {
        id: 4,
        name: 'New border 4',
        url: 'https://cdn.pixabay.com/photo/2016/06/23/08/55/frame-1474875_1280.png',
        cost: 27
      }]
    }
  },
  methods: {
    addBorder: function (index) {
      let choosenBorder = this.borders[index]
      let borderUrl = choosenBorder.url
      let borderPrise = choosenBorder.cost
      let borderName = choosenBorder.name
      bus.$emit('borderChosen', {borderUrl, borderPrise, borderName})
    }
  }
}
</script>

<style scoped>
  .is-centered {
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .border-img {
    width: 95%;
    height: 95%;
  }

  .border-list {
    list-style-type: none;
    -webkit-padding-start: 0px;
  }
</style>

