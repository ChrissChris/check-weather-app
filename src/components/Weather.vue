<template>
  <v-card
    :loading="loading"
    class="mx-auto my-12"
    max-width="500"
    color="#616161"
    height="700"
    elevation="10"
  >
    <v-card-text class="temperature-displaying">
      <h2 class="todayWeatherText">Today Weather</h2>
      <div v-if="kalvinTemperatureToday" class="temperature-text-wraper">
        <h1 class="celzius-temperature-display">{{ celciusTemperature }} °C</h1>

        <p class="positive-day-wishing">Have a nice day</p>

        ✨
      </div>
    </v-card-text>

    <v-text-field
      v-model="cityName"
      label="Please type your city name..."
      :rules="rules"
      hide-details="auto"
    ></v-text-field>

    <v-card-actions>
      <v-btn
        @click="receiveApiData"
        class="check-button"
        x-large
        color="success"
        dark
      >
        CHECK
      </v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
import axios from "axios";

export default {
  name: "Weather",
  data() {
    return {
      apiKey: "7814065530a2a625ade135ff3305cf1f",
      kalvinTemperatureToday: null,
      celciusTemperature: null,
      cityName: null,
      temperatureCityLocation: null,
    };
  },

  methods: {
    receiveApiData() {
      axios
        .get(
          `https://api.openweathermap.org/data/2.5/weather?q=${this.cityName}&appid=${this.apiKey}`
        )
        .then((responce) => {
          /* The command will receive only the temperature data from the API */

          this.kalvinTemperatureToday = responce.data.main.temp;

          /*  The row bellow will convert the received temperature data from the API from Kalvin to Celzius and asign it to celziusTemperature*/

          this.celciusTemperature = Math.round(
            this.kalvinTemperatureToday - 273.15
          );
        })
        .catch(() => {
          console.log("Please come back later, thank you :)");
        });
    },
  },
};
</script>

<style scoped>
.celzius-temperature-display {
  margin-top: 29px;
  margin-bottom: 29px;
}
.check-button {
  margin: auto;
  margin-top: 50px;
}
.temperature-displaying {
  margin-bottom: 100px;
}
.temperature-text-wraper {
  text-align: center;
  margin-top: 100px;
  font-size: 37px;
  color: white;
}

.todayWeatherText {
  text-align: center;
  color: white;
}
#temperatureLocation {
  font-size: 29px;
}
#positive-day-wishing {
  margin-top: 10px;
  font-size: 30px;
  font-style: normal;
  font-weight: bold;
}
</style>
