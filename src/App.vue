<template>
  <img alt="Vue logo" src="./assets/uber-eats-logo.png" id="logo">
  <RestaurantRow v-for="(card, index) in 9" :key="index" />
</template>

<script>

import RestaurantRow from './components/RestaurantRow.vue'

export default {
  name: 'App',
  components: {
    RestaurantRow
  }
}
</script>

<style>
@import url('./style/reset.css');
@import url('https://fonts.googleapis.com/css?family=Roboto:100,300,400,500,700,900');
#app {
  font-family: 'Roboto', sans-serif;
}

#logo {
  width: 100px;
  margin: 20px 20px;

}
</style>
