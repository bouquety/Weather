<template>
<div id="app">


<b-container class="meteo">
    <b-row>
  <b-col v-for="(item, index) in weather.daily" :key="index" cols="3">

    <div class="localisationDate">
      <div class="localisation">Paris</div>
      <div class="date">{{date[index]}}</div>
    </div>
    <div class="temperatureTemps">
      <div class="temperature"> {{ Math.round(weather.daily[index].temp.day) }}</div>
      <div class="temps" v-if="weather.daily[index].weather[0].main=='Clouds' ">Nuageux</div>
      <div class="temps" v-else>Pluie</div>
    </div>

</b-col>




 
  </b-row>

</b-container>
</div>
</template>

<script>
export default {
  name:'app',
  data(){
    this.api_key = process.env.api_key
    return {
      url_weather: 'https://api.openweathermap.org/data/2.5/onecall?lat=48.861&lon=2.346&units=metric&exclude=hourly,alerts,minutely&appid='+this.api_key,
      date: ['Lundi','Mardi','Mercredi','Jeudi','Vendredi','Samedi','Dimanche','Lundi'],
      weather:{},
    } 
  },
    mounted(){    
      this.getWeather()
    },
  methods: {
    getWeather (){
        this.$axios.$post(this.url_weather)
        .then(resp => {
            this.weather= resp
        })
        .catch(err => {
            console.log(err)
        });
    }
    }
}
</script>

<style scoped>
#app{
  background-image: url("../static/blue-blue-blue-gradation-wallpaper-preview.jpg");
  height: 100vh;
  background-image: linear-gradient(to bottom, rgba(0,0,0,0.25),rgba(0,0,0,0.75));
}

.localisationDate .localisation{
  color: #fff;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}

.localisationDate .date{
    color: #fff;
  font-size: 22px;
  font-weight: 300;
  text-align: center;
  font-style: italic;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}

.temperatureTemps{
  text-align: center;
}

.temperatureTemps .temperature{
  display: inline-block;
  padding: 10px 25px;
  color: #fff;
  font-size: 93px;
  font-weight: 900;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  margin: 30px 0px;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}

.temperatureTemps .temps{
  color: #fff;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
</style>