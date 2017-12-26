<template>
  <div class="store">
    <h1>{{ title }}</h1>
    <p>{{ msg }}</p>
    <ul class="tree-list">
        <li v-for="image in images" class="card border"><img v-bind:src="image.url" v-on:click="addTree(src)" class="tree-img"></li>
    </ul>
  </div>
</template>

<script>

import {bus} from '../main'

export default {
  name: 'Store',
  data () {
    return {
      title: 'Оберіть зображення',
      msg: 'Для почтку оберіть онову, тіло малюнка, на який ви і ваші гості будуть лишати відбитки пальців з побажаннями.',
      images: [{
        name: 'New title',
        url: 'https://i.pinimg.com/originals/e5/f7/3a/e5f73a614cb19675b248792d56276450.png',
        cost: 700
      }, {
        name: 'New title 2',
        url: 'http://www.pngall.com/wp-content/uploads/2016/03/Tree-Free-Download-PNG.png',
        cost: 750
      }, {
        name: 'New title 3',
        url: 'http://www.freepngimg.com/download/tree/6-2-tree-free-png-image.png',
        cost: 650
      }, {
        name: 'New title 4',
        url: 'https://cdn.pixabay.com/photo/2016/09/02/06/26/ficus-1638376_1280.png',
        cost: 700
      }]
    }
  },
  methods: {
    addTree: function (src) {
      let imageUrl = '../../src/assets/logo.png'
      console.log(src)
      bus.$emit('treeChosen', imageUrl)
    }
  }
}
</script>

<style scoped>
  .tree-img {
    width: 100%;
    height: 100%;
  }

  .tree-list {
    list-style-type: none;
    -webkit-padding-start: 0px;
  }
</style>
