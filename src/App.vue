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

      <div class="choosen-section">
        <keep-alive>
          <component v-bind:is="component"></component>
        </keep-alive>
      </div>
      
      <div class="result-section overlay"><Cart/></div>
      <div class="footer">
        <hr/>
        <p class="text-r">Total prise: <span class="is-green"><span class="f-lg">{{ totalPrise }}</span> грн.</span></p></div>
    </div>
  </div>
</template>

<script>
import Cart from './components/Cart'
import Store from './components/Store'
import Border from './components/Border'
import Signs from './components/Signs'
import Colors from './components/Colors'
import {bus} from './main'

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
      component: 'Store',
      treePrise: 0,
      borderPrise: 0
    }
  },
  computed: {
    totalPrise: function () {
      return this.treePrise + this.borderPrise
    }
  },
  created () {
    bus.$on('treeChosen', (data) => {
      this.treePrise = data.treePrise
    })
    bus.$on('borderChosen', (data) => {
      this.borderPrise = data.borderPrise
    })
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
  grid-template-rows: 55px auto 55px;
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

.element-description {
  text-align: left;
  margin: 0 16px;
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

  .card-sm {
    width: 150px;
    height: 150px;
    display: inline-block;
    margin: 10px 10px;
    box-sizing: border-box;
  }

  .menu {
    list-style-type: none;
    -webkit-padding-start: 0px;
    display: flex;
    justify-content: space-around;
  }

  .btn {
    padding: 8px 16px;
    border-radius: 14px;
    border: none;
    font-size: 1rem;
  }

  .btn:focus {
    outline: none;
  }

  .btn-primary {
    background-color: #36c742;
    color: #ffffff;
    font-weight: 600;
  }

  .btn-primary:active {
    background-color: #ffffff;
    color: #36c742;
    font-weight: 600;
  }

  .btn-lg {
    text-transform: uppercase;
  }

  .is-centered {
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .is-green {
    color: #36c742;
  }

  .text-r {
    text-align: right;
  }

  .f-lg {
    font-size: 1.5em;
    font-weight: 600;
  }
</style>
