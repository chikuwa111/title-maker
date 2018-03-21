<template>
  <div id="app">
    <h1>称号メーカー</h1>
    <p>モンハンの称号もどきを作れます</p>
    <Maker
      v-for="(result, index) in results"
      :key="index"
      :clicked="result.clicked"
      :text="result.text"
      :handler="onMakerClick(index)"
    />
    <div v-if="done">
      <p>完成！</p>
      <button class="btn" @click="reset">リセットする</button>
    </div>
  </div>
</template>

<script>
import Maker from './components/Maker'
import { titleList } from './constants'

export default {
  name: 'App',
  components: {
    Maker
  },
  data() {
    return {
      results: [
        { clicked: false, text: '' },
        { clicked: false, text: '' },
        { clicked: false, text: '' }
      ],
      list: titleList
    }
  },
  computed: {
    done: function() {
      return this.results.reduce((tmpDone, result) => tmpDone && result.clicked)
    }
  },
  methods: {
    onMakerClick(index) {
      return () => {
        if (this.results[index].clicked) return
        const randint = Math.floor(Math.random() * this.list.length)
        this.results = [
          ...this.results.slice(0, index),
          { clicked: true, text: this.list[randint] },
          ...this.results.slice(index + 1)
        ]
      }
    },
    reset() {
      this.results = this.results.map(() => ({
        clicked: false,
        text: ''
      }))
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
  margin-top: 30px;
}

/* 以下 https://saruwakakun.com/html-css/reference/buttons から拝借しました */

.btn {
  font-size: 20px;
  position: relative;
  display: inline-block;
  padding: 0.5em 0.75em;
  text-decoration: none;
  color: #fff;
  background: #03a9f4;
  border: solid 1px #0f9ada;
  border-radius: 4px;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2);
  text-shadow: 0 1px 0 rgba(0, 0, 0, 0.2);
}

.btn:active {
  border: solid 1px #03a9f4;
  box-shadow: none;
  text-shadow: none;
}
</style>
