<template>
  <div class="home">
    <div class="header">
      <img
        src="https://d3i4yxtzktqr9n.cloudfront.net/web-eats-v2/ee037401cb5d31b23cf780808ee4ec1f.svg"
        alt="logo Uber eats"/>
      <div class="wrapper-input">
        <input
          type="text"
          placeholder="De quoi avez-vous envie?"
          v-model="user_search_restaurant"/>
        <div class="search">
          <router-link v-for="(restaurant, i) in search_restaurant" :key="i" :to="{name: 'Restaurant', params: {name: restaurant.name}}">
            <div class="container-restaurant-search">
              <div class="wrapper-img">
                <img :src="restaurant.image" alt="search" />
              </div>
              <p>{{ restaurant.name }}</p>
            </div>
        </router-link>
        </div>
      </div>
    </div>
    <div class="banner"></div>
    <RestaurantRow
      v-for="(data, i) in data_restaurant"
      :key="i"
      :three_restaurant="data"
    />
  </div>
</template>

<script>
import BDD from "../bdd";
import { onMounted, ref, watch } from "vue";
import RestaurantRow from "../components/RestaurantRow.vue";

export default {
  name: "FirstPage",
  components: {
    RestaurantRow,
  },
  setup() {
    class Restaurant {
      constructor(name, image, note, drive_time) {
        this.name = name;
        this.image = image;
        this.note = note;
        this.drive_time = drive_time;
      }
    }

    let data_restaurant = ref([]);
    let all_restaurant = [];

    const makeDataRestaurant = () => {
      let three_restaurant = [];
      for (const restaurant of BDD) {
        const new_restaurant = new Restaurant(
          restaurant.name,
          restaurant.image,
          restaurant.note,
          restaurant.drive_time
        );
        all_restaurant.push(new_restaurant);
        if (three_restaurant.length === 2) {
          three_restaurant.push(new_restaurant);
          data_restaurant.value.push(three_restaurant);
          three_restaurant = [];
        } else {
          three_restaurant.push(new_restaurant);
        }
      }
    };
    let user_search_restaurant = ref("");
    let search_restaurant = ref([]);
    watch(user_search_restaurant, (newValue) => {
      let regex = RegExp(newValue.toLowerCase());
      let new_search_restaurant = all_restaurant.filter((restaurant) =>
        regex.test(restaurant.name.toLowerCase())
      );
      search_restaurant.value = new_search_restaurant;
     newValue == 0 ?  search_restaurant.value = [] : search_restaurant.value = new_search_restaurant;
    }),
      onMounted(makeDataRestaurant);
    return {
      data_restaurant,
      user_search_restaurant,
      search_restaurant,
    };
  },
};
</script>

<style lang="scss">
.home {
  .header {
    height: 120px;
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: space-between;
    img {
      width: 200px;
    }
    .wrapper-input {
      position: relative;

      input {
        background-color: #f6f6f6;
        width: 400px;
        height: 60px;
        border-radius: 5px;
        border: none;
        padding-left: 20px;
        outline: none;
      }
      .search {
        position: absolute;
        top: 100%;
        width: 100%;
        background-color: #ffffff;


        .container-restaurant-search{
         display: flex;
         align-items: center;
         padding: 10px;

         &:hover {
            background-color: #f6f6f6;
         }
        }

        .wrapper-img{
          height:60px;
          width: 60px;
          margin-right: 25px;
          overflow: hidden;
          border-radius: 50%;
        }
        img{
          height: 100%;
          width: auto;
        }
      }
    }
  }
  .banner {
    height: 200px;
    width: 100%;
    background-image: url("https://d3i4yxtzktqr9n.cloudfront.net/web-eats-v2/9b21aa66b4922ae2.png");
    background-size: cover;
    background-position: center center;
    margin-bottom: 20px;
  }
}
</style>
