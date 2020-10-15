<template>
  <div id="app">
    <AsteroidGrid :asteroids="asteroids" header="Near-Earth Objects" />
  </div>
</template>

<script>
import AsteroidGrid from './components/Asteroids.vue'
import axios from 'axios'

export default {
  name: 'app',
  components: {
    AsteroidGrid
  },
  data() {
      return {
        asteroids: []
      }
  },            
  created: function () {
      this.fetchAsteroids(0);
  },
  methods: {
      fetchAsteroids: function (days=0) {
          var apikey = 'lNNfzKOycBvSRvRgHNU5SXHxAYmEFQ0AxTfylr1x';
                var start_date = new Date();
                var end_date = new Date();
                end_date.setDate(start_date.getDate()+days);
                var url = 'https://api.nasa.gov/neo/rest/v1/feed?start_date=' + start_date.toISOString().split('T')[0] + '&end_date=' + end_date.toISOString().split('T')[0] + '&api_key=' + apikey;
          axios.get(url)
              .then(res => {
                this.asteroids=[];                                       
                  for(var i = start_date; i <= end_date; (i.setDate(i.getDate()+1))){
                            for(var j = 0; j < res.data.near_earth_objects[i.toISOString().split('T')[0]].length ; j++) {
                                this.asteroids.push ( res.data.near_earth_objects[i.toISOString().split('T')[0]][j] );
                            }
                        }
              });
      },
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

  button{
      transition: 0.2s ease-out;
      border: 1px solid white;
      background-color: inherit;
      color: inherit;
      font-family: inherit;
      font-weight: inherit;
      padding: 20px 40px;
      border-radius: 60px;
      font-size: 1em;
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
</style>
