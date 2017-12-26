<template>
  <div id="app">
    <div class="container border">
      <div class="header">
        <nav>
          <ul class="menu">
            <li v-on:click="component = 'Store'">1 Зображенння</li>
            <li v-on:click="component = 'Border'">2 Рамка</li>
            <li v-on:click="component = 'Signs'">3 Підписи</li>
            <li v-on:click="component = 'Colors'">4 Колір Відбитків</li>
          </ul>
        </nav>
        <hr/>
      </div>
      <div class="choosen-section"><component v-bind:is="component"></component><hr/></div>
      <div class="result-section overlay"><Cart/></div>
      <div class="footer"><h2>Total prise:</h2></div>
    </div>
  </div>
</template>

<script>
import Cart from './components/Cart'
import Store from './components/Store'
import Border from './components/Border'
import Signs from './components/Signs'
import Colors from './components/Colors'

export default {
  name: 'app',
  components: {
    Cart,
    Store,
    Border,
    Signs,
    Colors
  },
  data () {
    return {
      component: 'Store'
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

hr {
  -webkit-margin-before: 0;
  -webkit-margin-after: 0;
}

.container {
  height: 100%;
  display: grid;
  grid-template-columns: auto 300px;
  grid-template-rows: 100px auto 100px;
  grid-template-areas:
  "h r"
  "c r"
  "f r";
}

.header {
  grid-area: h;
}

.choosen-section {
  grid-area: c;
}

.result-section {
  grid-area: r;
}

.footer {
  grid-area: f;
}

.border {
  border-radius: 7px;
  border: 1px solid #9f9999;
}

.overlay {
    height: 100%;
    z-index: 0;
    background: rgba(177, 171, 171, 0.25);
}

 .card {
    width: 200px;
    height: 250px;
    display: inline-block;
    margin: 10px 10px;
    box-sizing: border-box;
  }

  .card:hover {
    border: 3px solid #36c742;
  }
</style>
