<template>
  <div class="signing">
    <div class="element-description">
      <h2>Підписи</h2>
      <p>Персоналізуйте ваше дерево побажань; зверху та знизу малюнка є спеціальні поля, 
        які можна заповнювати за бажанням - вписати ім'я винуватця події, особливі побажання,
        вказати дату, або логотип компанії.
      </p>
      <div class="inputs">
        <div class="singl-input">
          <input v-model.lazy="header" type="text" placeholder="Крутий заголовок">
          <label>Заголовок малюнку</label>
        </div>
        <div class="singl-input">
          <input v-model.lazy="body" type="text" placeholder="Марічка та Кіндрат">
          <label>Підпис</label>
        </div>
        <div class="singl-input">
          <input v-model.lazy="date" type="text" placeholder="32 січня 2017">
          <label>Дата події</label>          
        </div>
      </div>

      <div class="sign-font" >
        <h3>Доступні шрифти</h3>
        <ul>
          <li class="inline-b" v-for="(font, index) in fonts">
            <button class="btn btn-primary" v-on:click="addFont(index)">{{font}}</button>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>

import {bus} from '../main'

export default {
  name: 'Signs',
  data () {
    return {
      header: '',
      body: '',
      date: '',
      fonts: ['Ariston', 'DaVinci', 'Brody']
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
  },
  methods: {
    addFont: function (index) {
      bus.$emit('fontChosen', this.fonts[index])
    }
  }
}
</script>

<style scoped>
.signs-title {
  -webkit-margin-before: 1em;
  -webkit-margin-after: 1em;
}

.singl-input {
  margin: 16px 0;
}

input {
  border-radius: 14px;
  height: 32px;
  border: rgb(163, 163, 163) 1px solid;
  padding: 0 8px;
  font-size: 14px;
}
input:focus {
  outline: none;
}

label {
  margin-left: 16px;
  font-size: 16px;
  font-family: Arial, serif;
  font-weight: 600;
}

ul {
  list-style-type: none;
  -webkit-padding-start: 0px;
}

.inline-b {
  display: inline-block;
  margin-right: 16px;
}
</style>

