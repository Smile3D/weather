<template>
  <div class="home">
    <v-container>
      <div class="title-block">
        <h1><span class="label">Город:</span> {{ weathers.location.name }}</h1>
        <h2><span class="label">Страна:</span> {{ weathers.location.country }}</h2>
        <h2><span class="label">Регион:</span> {{ weathers.location.region }}</h2>
      </div>

      {{ weathers.location.localtime }}
      {{ weathers.current.condition.text }}
      <img :src="weathers.forecast.forecastday[0].hour[0].condition.icon" alt="">


      <v-card>
        <v-toolbar
            color="cyan"
            dark
            flat
        >
          <v-toolbar-title>

          </v-toolbar-title>
          <v-spacer></v-spacer>
          <template v-slot:extension>
            <v-tabs
              v-model="tab"
              align-with-title
            >
              <v-tabs-slider color="yellow"></v-tabs-slider>
              <v-tab
                v-for="item in weathers.forecast.forecastday[0].hour[0].condition"
                :key="item"
              >
                {{ item.text }}

<!--                {{ item }}-->
              </v-tab>
            </v-tabs>
          </template>
        </v-toolbar>
        <v-tabs-items v-model="tab">
          <v-tab-item
            v-for="item in items"
            :key="item"
          >
            {{ item }}
            <v-card flat>
              <v-card-text v-text="text"></v-card-text>
            </v-card>
          </v-tab-item>
        </v-tabs-items>
      </v-card>
    </v-container>

  </div>
</template>

<script>
export default {
  name: 'Home',
  data() {
    return {
      weathers: [],
      tab: null,
      items: [
        'web', 'shopping', 'videos', 'images', 'news',
      ],
      text: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.',
    }
  },
  mounted() {
    fetch("http://api.weatherapi.com/v1/forecast.json?key=94b63fdc98224d41a69164709211807&q=Cambridge&days=3&lang=ru&aqi=yes&alerts=no")
        .then(data => data.json())
        .then(data => (console.log(this.weathers = data)))
  }
}
</script>
<style lang="scss">
.title-block {
  text-align: center;

  span {
    color: #00bcd4;
  }
}

h1 {
  text-transform: uppercase;
}
</style>
