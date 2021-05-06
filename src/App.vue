<template>
<div id="app" v-if="weather.main" :class=" 
   weatherBackGround(weather.weather[0].main)">
   <header >
    <p class="date">{{dateBuilder()}}</p>
     <div class="search-box">
      <i class="fas fa-search"  />
       <input type="text" 
       class="search-bar" 
       placeholder="Search city weather" 
       v-model="searchCity"
       @keypress="getWeather"/>
     </div>
   </header>
  <main >
     <div class="weather-wrap" >
       <h1 class="location">{{weather.name}}</h1>
       <p class="weather">{{titleCase(weather.weather[0].description)}}</p>
       <p class="temp">{{Math.round(weather.main.temp)}}°C</p>
       <img :src="getImgUrl(weather.weather[0].main.toLowerCase())">
       <div class="temp-box">
         <p>min:{{Math.round(weather.main.temp_min)}}°C</p>
          <p>max:{{Math.round(weather.main.temp_max)}}°C</p>
       </div>
       <div class="row-box">
       <div class="feel-like-box">
         <p>{{Math.round(weather.main.feels_like)}}°C</p>
         <p>Feels like</p>
       </div>

        <div class="humidity-box">
         <p>{{weather.main.humidity}}%</p>
         <p>Humidity</p>
       </div>
       </div>
     </div>
   </main>
</div>

</template>

<script>
import axios from "axios";
export default {
  name: 'App',
   data() {
     return {
       api_key:'ff1f8b66d99f2c221671c3bedc1212a7',
       url_base:'http://api.openweathermap.org/data/2.5/',
       searchCity:undefined,
       myCity:'Barcelona',
       weather:{}
     }
   },

   mounted: async function(){
     const { data } = await  axios.get(`${this.url_base}weather?q=${this.myCity}&appid=${this.api_key}&units=metric`);
      this.weather = data;
   },

   methods:{
     getWeather: async function (e){
       if(e.key === 'Enter'){ 
       const { data } = await axios.get(`${this.url_base}weather?q=${this.searchCity}&appid=${this.api_key}&units=metric`)
       this.searchCity='';
       this.weather = data;
       console.log(data);
       }
     },

     dateBuilder(){
      const dateNow = new Date();
      const months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
      const days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
      const day = days[dateNow.getDay()];
      const date = dateNow.getDate();
      const month = months[dateNow.getMonth()];
      const year = dateNow.getFullYear();
      return `${day} ${date} ${month} ${year}`;   
     },


getImgUrl(icon){
   return require("./assets/images/"+icon+".png");
},
 titleCase(str) {
 const newStr = str.slice(0,1).toUpperCase() + str.slice(1).toLowerCase();
    return newStr;
},
   weatherBackGround(weather){
     switch(weather){
       case 'Clear':
         return 'clear';
        case 'Rain':
          return 'rain';
        case 'Clouds':
          return 'clounds'
        case 'Mist':
          return 'mist'
        case 'Haze':
          return 'haze'
       default:
         return 'default-color';     }
   }
    
   }


}
</script>

<style>
@import './assets/styles.css';
</style>
