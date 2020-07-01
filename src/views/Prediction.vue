<template>
  <div
    class="d-flex flex-column justify-content-center align-items-center"
    style="height: 80vh;"
  >
    <div class="p-0 justify-content-center">
      <h1 class="text-center">Cricket Weather</h1>
      <h2 class="text-center" v-if="!APIResult.length">
        Enter Weather Details
      </h2>
      <h1 class="text-center" v-else style="font-size:4rem">{{ APIResult }}</h1>
    </div>
    <div class="p-2">
      <form @submit.prevent>
        <div class="form-row" style="max-width:500px">
          <div class="form-group col-12">
            <label for="weather">Weather</label>
            <select
              v-model.trim="weatherdata.weather"
              class="form-control"
              id="weather"
            >
              <option value="2" selected>Sunny</option>
              <option value="0" selected>Overcast</option>
              <option value="1" selected>Rainy</option>
            </select>
          </div>
          <div class="form-group col-12">
            <label for="weather">Temperature</label>
            <select
              v-model.trim="weatherdata.temperature"
              class="form-control"
              id="weather"
            >
              <option value="1" selected>Hot</option>
              <option value="2" selected>Mild</option>
              <option value="0" selected>Cool</option>
            </select>
          </div>

          <button
            @click="predict"
            type="button"
            class="btn btn-primary btn-lg btn-block"
          >
            Submit
          </button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import { getAPI } from "@/axios";
export default {
  name: "Posts",
  data() {
    return {
      weatherdata: {
        weather: "",
        temperature: ""
      },
      APIResult: []
    };
  },
  methods: {
    predict() {
      getAPI
        .get("/cricket", {
          params: {
            weather: this.weatherdata.weather,
            temperature: this.weatherdata.temperature
          }
        })
        .then(response => {
          console.log("Recieved data successfully");
          const result = response.data;
          if (result == 0) {
            this.APIResult = "No Cricket today";
          } else {
            this.APIResult = "Its good for Cricket today";
          }
          console.log(response.data);
        })
        .catch(err => {
          console.log(err);
        });
    }
  }
};
</script>

<style>
</style>

