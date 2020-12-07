<template>
  <div id="app">
    <AsteroidGrid :asteroids="asteroids" header="Near-Earth Objects" />
    <Sunrise :sunrise="sunrise" :sunset="sunset" />
  </div>
</template>

<script>
import AsteroidGrid from './components/Asteroids.vue'
import Sunrise from './components/Sunrise.vue'
import axios from 'axios'

export default {
  name: 'app',
  components: {
    AsteroidGrid,
    Sunrise
  },
  data() {
      return {
        asteroids: [],
        sunrise: new Date(),
        sunset: new Date(),
        latitude: 40.7128,
        longitude: 74.0060,
        time: new Date()
      }
  },            
  created: function () {
      this.fetchAsteroids(0);
      this.getLoc();
      this.getSunPos();
  },
  methods: {
      fetchAsteroids: function (days=0) {
          this.asteroids=[]; 
          var apikey = 'lNNfzKOycBvSRvRgHNU5SXHxAYmEFQ0AxTfylr1x';
                var start_date = new Date();
                var end_date = new Date();
                end_date.setDate(start_date.getDate()+days);
                var url = 'https://api.nasa.gov/neo/rest/v1/feed?start_date=' + start_date.toISOString().split('T')[0] + '&end_date=' + end_date.toISOString().split('T')[0] + '&api_key=' + apikey;
          axios.get(url)
              .then(res => {
                  for(var i = start_date; i <= end_date; (i.setDate(i.getDate()+1))){
                            for(var j = 0; j < res.data.near_earth_objects[i.toISOString().split('T')[0]].length ; j++) {
                                this.asteroids.push ( res.data.near_earth_objects[i.toISOString().split('T')[0]][j] );
                            }
                        }
              });
      },
      getLoc: function (){
        var loc_apikey = 'df960888abe04b86a99cebb28c932f46';
        var url = 'https://api.ipgeolocation.io/ipgeo?apiKey=' + loc_apikey;
        axios.get(url)
          .then(res => {
            this.latitude = res.data.latitude;
            this.longitude = res.data.longitude;
            this.getSunPos();
          })
      },
      getSunPos: function(){
        var url = 'https://api.sunrise-sunset.org/json?lat='+ this.latitude + "&lng=" + this.longitude + "&formatted=0";
        axios.get(url)
        .then(res => {
            this.sunrise = new Date(res.data.results.sunrise);
            this.sunset = new Date(res.data.results.sunset);
          })
        
      }
  }
}
</script>

<style>
  @keyframes fade-in{
    from {opacity: 0;}
    to {opacity: 1;}
  }
  [v-cloak] {
    display: none;
  }
  body{
    animation: fade-in 1.5s ease-in;
  }
  button{
      transition: 0.2s ease-out;
      border: 1px solid white;
      background-color: inherit;
      color: inherit;
      font-family: inherit;
      font-weight: inherit;
      padding: 15px 20px;
      border-radius: 60px;
      font-size: 1rem;
  }
  button:hover{
      color: #18AB39;
      border: 1px solid #18AB39;
  }
  button:focus{
      outline: none;
  }
  .btn-selected{
      color: #18AB39;
      border: 1px solid #18AB39;
  }
@media only screen and (min-width: 500px) {
  button{
      padding: 20px 40px;
      border-radius: 60px;
      font-size: 1em;
  }
}
</style>
