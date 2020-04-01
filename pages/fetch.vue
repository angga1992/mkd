<template>
  <div>
    <table class="tg">
      <tr>
        <th class="tg-0pky">ID</th>
        <th class="tg-0pky">currentTemp</th>
        <th class="tg-0pky">minTemp</th>
        <th class="tg-0pky">maxTemp</th>
        <th class="tg-0pky">pressure</th>
        <th class="tg-0pky">humidity</th>
        <th class="tg-0pky">wind</th>
        <th class="tg-0pky">overcast</th>
        <th class="tg-0pky">icon</th>
        <th class="tg-0pky">sunrise</th>
        <th class="tg-0pky">sunset</th>
      </tr>

      <tr>
        <td class="tg-0pky">{{id}}</td>
        <td class="tg-0pky">{{currentTemp}}</td>
        <td class="tg-0pky">{{minTemp}}</td>
        <td class="tg-0pky">{{maxTemp}}</td>
        <td class="tg-0pky">{{pressure}}</td>
        <td class="tg-0pky">{{humidity}}</td>
        <td class="tg-0pky">{{wind}}</td>
        <td class="tg-0pky">{{overcast}}</td>
        <td class="tg-0pky">{{icon}}</td>
        <td class="tg-0pky">{{sunrise}}</td>
        <td class="tg-0pky">{{sunset}}</td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  layouts: 'sabeb',
  data() {
    return {
      post: [],
      currentTemp: '',
      minTemp: '',
      maxTemp: '',
      sunrise: '',
      sunset: '',
      pressure: '',
      humidity: '',
      wind: '',
      overcast: '',
      icon: '',
      id: ''
    }
  },
  mounted() {
    this.getWeather()
  },
  methods: {
    getWeather() {
      let url = "http://api.openweathermap.org/data/2.5/weather?q=bandung&?units=metric&APPID=dc2a9f0f840b61b7d18a65d8a46fbcf5";
      this.$axios
        .get(url)
        .then(response => {
          this.id = response.data.id
          this.currentTemp = response.data.main.temp;
          this.minTemp = response.data.main.temp_min;
          this.maxTemp = response.data.main.temp_max;
          this.pressure = response.data.main.pressure;
          this.humidity = response.data.main.humidity + '%';
          this.wind = response.data.wind.speed + 'm/s';
          this.overcast = response.data.weather[0].description;
          this.icon = "images/" + response.data.weather[0].icon.slice(0, 2) + ".svg";
          this.sunrise = new Date(response.data.sys.sunrise * 1000).toLocaleTimeString("en-GB").slice(0, 4);
          this.sunset = new Date(response.data.sys.sunset * 1000).toLocaleTimeString("en-GB").slice(0, 4);
          this.post = response
        })
        .catch(error => {
          console.log(error);
        })
    }
  }
}
</script>

<style>
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;border-color:black;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;border-color:black;}
.tg .tg-0pky{border-color:inherit;text-align:left;vertical-align:top}
</style>