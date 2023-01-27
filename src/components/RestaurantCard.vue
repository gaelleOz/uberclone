<template>
  <div class="restaurant-card">
    <div :style="changeBackground" class="restaurant-image"></div>
    <div class="restaurant-information">
      <div class="top">
        <p class="name">{{ info_restaurant.name }}</p>
        <p class="note">
          <span>{{ info_restaurant.note }}</span>
        </p>
      </div>
      <p class="time">{{ info_restaurant.drive_time }}</p>
    </div>
  </div>
</template>

<script>
import { computed } from "vue";
export default {
  name: "RestaurantCard",
  props: {
    info_restaurant: {
      type: Object,
    },
  },
  setup(props) {
    const changeBackground = computed(() => {
      return {
        backgroundImage: `url(${props.info_restaurant.image})`,
      };
    });
    return {
      changeBackground,
    };
  },
};
</script>

<style lang="scss">
.restaurant-card {
  width: 32%;
  height: 30vh;
  background-color: #fff;
  border-radius: 5px;
  box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.1);
  margin: 10px;

  p {
    margin: 0;
  }

  .restaurant-image {
    height: 70%;
    background-image: url("https://cn-geo1.uber.com/image-proc/resize/eats/format=webp/width=550/height=440/quality=70/srcb64=aHR0cHM6Ly9kMXJhbHNvZ25qbmczNy5jbG91ZGZyb250Lm5ldC8zNzg4MDJiMC1jNTI4LTQ4MjktYjBiNS0wY2M2NDBkZjYzY2QuanBlZw==");
    background-size: cover;
    background-position: center;
  }

  .restaurant-information {
    .top {
      display: flex;
      justify-content: space-between;
      padding: 10px 15px;
      align-items: center;
    }

    .note {
      background-color: #eeeeee;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 30px;
      width: 30px;
      border-radius: 50%;
      padding: 3px;
      font-size: 0.8rem;
    }

    .time {
      padding: 0px 15px;
      font-size: 0.9em;
      color: #9b9b9b;
    }
  }
}
</style>
