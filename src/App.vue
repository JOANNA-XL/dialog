<template>
  <div id="app">
    <app-header></app-header>
    <app-input></app-input>
    <app-undone></app-undone>  
    <app-completed></app-completed>
    <app-cancelled></app-cancelled>
    <app-footer></app-footer>
  </div>
</template>

<script>
import appHeader from './components/header'
import appInput from './components/input'
import appUndone from './components/undone'
import appCompleted from './components/completed'
import appCancelled from './components/cancelled'
import appFooter from './components/footer'
export default {
  name: 'App',
  components:{
    appHeader,
    appInput,
    appUndone,
    appCompleted,
    appCancelled,
    appFooter
  }
}
</script>

<style>

</style>
