<template>
  <div class="root">
    <div class="weather-root">
      <input type="text" class="input-box" v-model="query" @keypress="getWeather"/>
      <div class="time">Local Time: {{ moment().format('h:mm a') }}</div>
      <div class="location">{{ location }}</div>
      <div class="temp-container">
        <span v-bind:class="{ hot: this.temperature >= 25, cold: this.temperature <= 15 }" class="temperature">{{ temperature }}<sup>°</sup>C</span>
      </div>
      <div class="weather">{{ weather }}</div>

      
    </div>
    
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import moment from 'moment'

@Component
export default class Weather extends Vue {
  moment = moment;
  query = "";
  location = "Vancouver";
  temperature = 0;
  weather = "";
  key = 'cd5a4272e32b5155ba22442cb4918473';
  base_url = 'https://api.openweathermap.org/data/2.5/weather?q=';

  mounted(){
    console.log(moment().format());
    fetch(this.base_url + "Vancouver" + '&APPID=' + this.key).then(res =>{
      return res.json();
    }).then(this.update);
    return;
  }

  getWeather(e){
    if(e.key != 'Enter')
      return
    fetch(this.base_url + this.query + '&APPID=' + this.key).then(res =>{
      return res.json();
    }).then(this.update);
    return;
  }

  update(res){
    console.log(res);
    this.location = res.name;
    this.temperature = parseInt((res.main.temp - 273.15).toFixed(0), 10);
    this.weather = res.weather[0].description;
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Montserrat&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Quicksand&display=swap');

.root {
  min-height: 100vh;
  background-image: url('https://images.unsplash.com/photo-1562633284-f7fc3fd08ff2?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1350&q=80');
}

.weather-root {
  padding: 20px;
  max-width: 500px;
  margin: auto;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-content: center;
}

.input-box {
  display: block;
  width: 100%;
  padding: 15px;
  font-size: 20px;

  color: #313131;
  appearance: none;
  border:none;
  outline: none;
  background: none;

  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 0px 16px 0px 16px;
  transition: 0.4s;
}

.location {
  margin-top: 40px;
  font-size: 30px;
  text-align: center;
  font-family: 'Quicksand', sans-serif;
  font-weight: 600;
}

.temp-container {
  display: flex;
  justify-content: center;
}

.temperature {
  margin: 40px 0;
  font-size: 80px;
  text-align: center;
  font-family: 'Montserrat', sans-serif;
  font-weight: 600;
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 10px;
  padding: 10px 25px;
}

.weather {
  font-size: 40px;
  text-align: center;
  font-family: 'Montserrat', sans-serif;
  font-weight: 600;
}

.time {
  margin-top: 40px;
  font-size: 40px;
  text-align: center;
  font-family: 'Montserrat', sans-serif;
  font-weight: 600;
}

.hot {
  color: firebrick;
}

.cold {
  color: cornflowerblue;
}
</style>
