<template>
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
</template>

<script>
  export default {
    name: 'Header',
    methods: {
      dateBuilder() {
        this.$parent.dateBuilder();
      },
      getWeather(){
         this.$parent.getWeather();
      }
    }
  }
</script>