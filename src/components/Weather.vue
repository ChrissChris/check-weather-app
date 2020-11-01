<template>
  <v-card
    :loading="loading"
    class="mx-auto my-12"
    max-width="500"
    color="#616161"
    height="700"
    elevation="10"
  >
    <v-card-text class="temperature-displaying-wraper">
      <h2 class="today-weather-heading-text">Today Weather</h2>
      <div v-if="kalvinTemperatureToday" class="temperature-data-wraper">
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
.temperature-displaying-wraper {
  margin-bottom: 7em;
}
.celzius-temperature-display {
  margin-top: 2em;
  margin-bottom: 1.5em;
}
.check-button {
  margin: auto;
  margin-top: 3em;
}

.temperature-data-wraper {
  text-align: center;
  margin-top: 4em;
  font-size: 2.5em;
  color: white;
}

.today-weather-heading-text {
  text-align: center;
  color: white;
}
#temperatureLocation {
  font-size: 29px;
}
.positive-day-wishing {
  margin-top: 3em;
  margin-bottom: 1em;
  font-size: 1em;
  font-style: normal;
  font-weight: bold;
}
</style>
