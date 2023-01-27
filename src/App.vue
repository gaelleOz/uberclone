<template>
  <FirstPage/>
</template>

<script>

import FirstPage from './page/FirstPage.vue'

export default {
  name: 'App',
  components: {
    FirstPage,
  }
}
</script>

<style>
@import url('./style/reset.css');
@import url('https://fonts.googleapis.com/css?family=Roboto:100,300,400,500,700,900');
#app {
  font-family: 'Roboto', sans-serif;
  padding: 0px 20px;
  margin: 0px 20px;
}
</style>
