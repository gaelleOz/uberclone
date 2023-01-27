<template>
  <p>{{ $route.params.name }}</p>
</template>

<script>

import BDD from "../bdd";
import { onMounted } from "vue";

export default {
  name: "RestaurantPage",
  setup() {
    onMounted(() => {
      console.log(BDD);
    });
  },
}
</script>

<style>

</style>
