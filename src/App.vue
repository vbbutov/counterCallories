<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <my-page></my-page>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component'
import MyPage from './views/Page.vue'

@Options({
  components: {
    MyPage
  }
})
export default class App extends Vue {}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
