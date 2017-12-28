<template>
  <div class="store">
    <div class="element-description">
      <h2>{{ title }}</h2>
      <p>{{ msg }}</p>
    </div>
    <ul class="tree-list">
        <li v-for="(image, index) in images" class="card border"><img :src="image.url" v-on:click="addTree(index)" class="tree-img"></li>
        <!-- <li v-for="image in images" class="card border"><img :src="image.url" :data-id="image.id" v-on:click="addTree" class="tree-img"></li> -->
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
        id: 1,
        name: 'New title',
        url: 'https://i.pinimg.com/originals/e5/f7/3a/e5f73a614cb19675b248792d56276450.png',
        cost: 700
      }, {
        id: 2,
        name: 'New title 2',
        url: 'http://www.pngall.com/wp-content/uploads/2016/03/Tree-Free-Download-PNG.png',
        cost: 750
      }, {
        id: 3,
        name: 'New title 3',
        url: 'http://www.freepngimg.com/download/tree/6-2-tree-free-png-image.png',
        cost: 650
      }, {
        id: 4,
        name: 'New title 4',
        url: 'https://cdn.pixabay.com/photo/2016/07/12/08/19/tree-1511608_1280.png',
        cost: 700
      }]
    }
  },
  methods: {
    addTree: function (index) {
      let choosenImage = this.images[index]
      let treeUrl = choosenImage.url
      let treePrise = choosenImage.cost
      let treeName = choosenImage.name
      bus.$emit('treeChosen', {treeUrl, treePrise, treeName})
    }
  }
}
</script>

<style scoped>
  .tree-img {
    width: 90%;
    height: 90%;
  }

  .tree-list {
    list-style-type: none;
    -webkit-padding-start: 0px;
  }
</style>
