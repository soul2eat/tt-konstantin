<template>
    <div id="app">
        <Main/>
        <App-view/>
    </div>
</template>

<script>
import Main from './components/Main.vue'
import AppView from './components/App-view'


export default {
  name: 'App',
  components: {
    Main,
    AppView
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Roboto:300,400,400i,500,700');

#app {
    font-family: 'Roboto';
    font-style: normal;
    font-weight: normal;
    display: flex;
    background: #F6F6F6;
    min-height: 100vh;
    max-width: 1440px;
}
body {
    margin: 0px;
}
</style>
