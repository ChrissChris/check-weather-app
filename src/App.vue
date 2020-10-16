<template>
  <div id="app">
    <v-app>
      <v-row>
        <v-col>
          <weather />
        </v-col>
      </v-row>
    </v-app>
  </div>
</template>

<script>
import Weather from "@/components/Weather"

export default {
  name: "App",

  components: {
    Weather,
  },
}
</script>
