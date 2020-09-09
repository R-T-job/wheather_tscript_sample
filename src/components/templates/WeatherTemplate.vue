<template>
  <div class="container">
    <Location v-bind="location"/>
    <Temperature v-bind="temperature"/>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import Location from '@/components/organism/Location.vue';
import Temperature from '@/components/organism/Temperature.vue';

import axios from 'axios'
import * as dotenv from "dotenv";

@Component({
  components: {
    Location,
    Temperature,
  },
})
export default class App extends Vue {
  private temperature: {
    tempCentigrade: number;
    tempratureDegree: number;
    tempratureDescription: string;
  } = {
    tempCentigrade: 0, 
    tempratureDegree: 0, 
    tempratureDescription: "" 
  };

  private location: {
    locationTimezone: string;
    wheatherIconSrc: string;
  } = {
    locationTimezone: "", 
    wheatherIconSrc: "",
  };
  /** ライフサイクルフック */
  public mounted(){
    if ( navigator.geolocation ) {
      navigator.geolocation.getCurrentPosition(position => {
        let lon: number = position.coords.longitude;
        let lat: number = position.coords.latitude;
        const appid = process.env.VUE_APP_APP_ID;
        const units: string = "metric"
        const apiURL:string = 'https://api.openweathermap.org/data/2.5/weather'

        axios.get(apiURL, {
          params: {
            lat: lat,
            lon: lon,
            units: units,
            appid: appid,
          }
        }).then(response => {
          console.log(response)
          const resDate = response.data

          // 気温取得
          this.temperature.tempCentigrade = resDate.main.temp
          this.temperature.tempratureDegree = this.temperature.tempCentigrade;

          // 天気詳細取得
          const description = resDate.weather[0].description;
          this.temperature.tempratureDescription = description;

          console.log(this.temperature)

          //　国、地域名取得
          const country = resDate.sys.country
          const name = resDate.name
          // 地域ごとの時間および天気
          this.location.locationTimezone = `${country}/${name}`;

          const icon = resDate.weather[0].icon;
          this.location.wheatherIconSrc = `http://openweathermap.org/img/wn/${icon}@2x.png`;

          console.log(this.location)
        })
        .catch(response => console.log(response))
        });
    } else {
      this.location.locationTimezone = "hey dis is not working because resons"
    }
  }
}
</script>

<style>
.container {
    height: 100vh;
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items:center;
    background: linear-gradient(rgb(47,150,163), rgb(48,62,143));
    font-family: sans-serif;
    color: white;
}
</style>