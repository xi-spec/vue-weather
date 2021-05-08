<template>
     <header >
    <p class="date">{{dateBuilder()}}</p>
     <div class="search-box">
      <i class="fas fa-search"  />
       <input type="text" 
       class="search-bar" 
       placeholder="Search city weather" 
       v-model="this.$parent.searchCity"
       v-on:keyup.enter="getWeather"/>
     </div>
   </header>
</template>

<script>
  export default {
    name: 'Header',
    methods: {
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
         getWeather(){
    this.$parent.getWeather()
     }
    }
  }
</script>