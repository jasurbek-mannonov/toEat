<script setup lang="ts">
import { ref } from 'vue';

interface Restaurant {
  name?: string,
  address?: string,
  status?: RestaurantStatus,
  dishes?: Dish[]
}

type RestaurantStatus = 
| 'Want To Try' | "Recommended" | "Do Not Recommended" | "Must Try"

const statusList = [
  'Want to try',
  'Recommended',
  'Do Not Recommended',
  'Must Try'
]


const restaurantList = ref<Restaurant[]>([]);
const newRestaurant = ref<Restaurant>({});

function addRestaurant() {
  restaurantList.value.push({
    name: newRestaurant.value.name,
    status: 'Want To Try',
    dishes: []
  })
}
</script>

<template>
  <main>
    <pre>
      {{ newRestaurant }}
    </pre>
    <form @submit.prevent="addRestaurant">
      <div>
        <label for="restaurant-name">Restaurant name</label>
        <input id="restaurant-name" v-model="newRestaurant.name" type="text" />
      </div>
      <div>
        <label for="restaurant-status">Restaurant status</label>
        <select name="restaurant-status" id="restaurant-status" v-model="newRestaurant.status">
          <option v-for="status in statusList" :value="status" :key="status">{{status}}</option>
        </select>
      </div>
      <button type="submit">Add Restaurant</button>
    </form>

    <ul>
      <li v-for="restaurant in restaurantList" :key="restaurant">{{ restaurant.name }}</li>
    </ul>
  </main>
</template>
