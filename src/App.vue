<template>
<div id="app" v-if="weather.weather" :class=" 
weather.weather[0].main.toLowerCase()">
  <Header  />
  <main >
     <div class="weather-wrap" >
       <h1 class="location">{{`${weather.name} ${weather.sys.country}`}}</h1>
       <p class="weather">{{titleCase(weather.weather[0].description)}}</p>
       <p class="temp">{{Math.round(weather.main.temp)}}°C</p>
       <img :src="getImgUrl(weather.weather[0].main.toLowerCase())">
       <div class="temp-box">
         <p>min: {{Math.round(weather.main.temp_min)}}°C</p>
          <p>max: {{Math.round(weather.main.temp_max)}}°C</p>
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
import Header from './components/header';
export default {
  name: 'App',
  components:{
    Header
  },
   data() {
     return {
       myCity:'Barcelona',
       searchCity:null,
       weather:{},
     }
   },

   mounted: async function(){
     const { data } = await  axios.get(`${process.env.VUE_APP_BASE_URL}weather?q=${this.myCity}&appid=${process.env.VUE_APP_BASE_KEY}&units=metric`);
      this.weather = data;
   },

   methods:{

       getWeather: async function (){
         const { data } = await axios.get(`${process.env.VUE_APP_BASE_URL}weather?q=${this.searchCity}&appid=${process.env.VUE_APP_BASE_KEY}&units=metric`)
         this.searchCity='';
         this.weather = data;
     },
  
      getImgUrl(icon){
        return require("./assets/images/"+icon+".png");
  },
   titleCase(str) {
     const newStr = str.slice(0,1).toUpperCase() + str.slice(1).toLowerCase();
     return newStr;
  },
    
   }


}
</script>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  ::placeholder { /* Chrome, Firefox, Opera, Safari 10.1+ */
    color: white;
    opacity: 1; /* Firefox */
  }
  
  :-ms-input-placeholder { /* Internet Explorer 10-11 */
    color: white;
  }
  
  ::-ms-input-placeholder { /* Microsoft Edge */
    color: white;
  }

  input{
      color:white;
  }

  img{
      max-height: 250px;
      margin: 20px;
  }

  body{
    font-family: 'montserrat', sans-serif;
    color: white;
  }
  
  main{
    width: 100vw;
    height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;

  }

  header{
  padding: 20px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  .date{
      padding: 10px;
  }         


  .clear{
    background-color:rgb(254,220,73)
  }
  .rain{
      background-color: rgb(24,159,253);
  }
  .clouds{
      background-color: rgb(101,123,207);
  }
  .mist{
    background: rgb(189,197,247);
    background: linear-gradient(0deg, rgba(189,197,247,1) 0%, rgba(218,229,241,1) 100%);
  }
  .haze{
    background: rgb(255,185,101);
    background: linear-gradient(0deg, rgba(255,185,101,1) 0%, rgba(218,229,241,1) 100%);
  }

  .defalut-color{
      background-color: rgb(40, 165, 56);
  }


 
.weather-wrap{
    display: flex;
    padding-top: 30px;
    flex-direction: column;
    align-items: center;
}

.weather-wrap > * {
    padding-bottom: 5px;
}

.temp{
    font-size: 30px;
}
  .temp-box{
      width: 200px;
      display: flex;
      justify-content: space-between;
  }

  .row-box{
    width: 200px;
    margin-top: 30px;
      display: flex;
      flex-direction: row;
      justify-content: space-between;
  }
.feel-like-box{
    display: flex;
    flex-direction: column;
    justify-content: center;

}

@media (min-width: 599px) {
 .weather-wrap{
   padding-top: 0px;
 }
}
</style>
