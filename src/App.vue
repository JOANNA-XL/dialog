<template>
  <div id="app">
    <app-header></app-header>
    <app-input></app-input>

    <app-footer></app-footer>
  </div>
</template>

<script>
import appHeader from './components/header'
import appInput from './components/input'

import appFooter from './components/footer'
export default {
  name: 'App',
  components:{
    appHeader,
    appInput,
    appFooter
  }
}
</script>

<style>

</style>
