<template>
    <div class = "NEO-container"> 
        <h1 style="fontSize: 12vw">ASTROSPACE</h1>  
        <h1>{{header}}</h1> 
        <div v-cloak v-if="numAsteroids > 0 " class="summary"> 
            <p>showing {{numAsteroids}} items</p> 
            <p>{{closestObject}} has the smallest miss distance.</p> 
        </div> 
        <div class="date-btn-container">
        <button @click="fetchAsteroids(0)" class="date-btn btn-selected" id="btn-today">Today</button>
        <button @click="fetchAsteroids(6)" class="date-btn" id="btn-week">This Week</button>
        </div>
        <table> 
            <thead> 
                <th>#</th> 
                <th>Name</th> 
                <th>Close Approach</th> 
                <th>Miss Distance</th> 
            </thead> 
                <tr v-for="(a, index) in asteroids" 
                    :key="a.neo_reference_id"> 
                    <td>{{index + 1}}</td> 
                    <td>{{a.name}}</td> 
                    <td>{{getCloseApproachDate(a)}}</td> 
                    <td> 
                                {{a.close_approach_data[0].miss_distance.kilometers}} km 
                    </td> 
                </tr> 
        
        </table>
            <p class="loading-text" v-cloak v-if="numAsteroids <= 0 "> Loading Asteroids...</p>  
        
        <!-- <h1>Sunrise in 2 hours</h1> -->
    </div>
</template>

<script>
    export default {
        props: ['asteroids', 'header'],
        data: function() {
            return {            
            }
        },  
        computed: {
            numAsteroids: function() {
                return this.asteroids.length;
            },
            closestObject: function() {
                var neosHavingData = this.asteroids.filter(function(neo) {
                    return neo.close_approach_data.length > 0;
                });                
                var simpleNeos = neosHavingData.map(function(neo) {
                    return {name: neo.name, miles: neo.close_approach_data[0].miss_distance.miles};        
                });
                var sortedNeos = simpleNeos.sort(function(a, b) {
                    return a.miles - b.miles;        
                });
                return sortedNeos[0].name;
            }    
        },  
        methods: {
            getCloseApproachDate: function (a) {
                if (a.close_approach_data.length > 0 && a.close_approach_data[0].close_approach_date_full!=null) {
                    return new Date(a.close_approach_data[0].close_approach_date_full + " EST").toLocaleString();   
                }
                else if(a.close_approach_data.length > 0 && a.close_approach_data[0].close_approach_date!=null){
                    return new Date(a.close_approach_data[0].close_approach_date).toUTCString().split('00:00:00 GMT')[0];
                }
                return 'N/A';
            },
            // getCloseApproachTime: function (a) {
            //     if (a.close_approach_data.length > 0) {
            //         return a.close_approach_data[0].close_approach_date_full;   
            //     }
            //     return 'N/A';
            // },
            fetchAsteroids: function (days) {
                if(days==0) {
                    document.getElementById("btn-week").classList.remove("btn-selected");
                    document.getElementById("btn-today").classList.add("btn-selected");
                }
                else if(days==6) {
                    document.getElementById("btn-today").classList.remove("btn-selected");
                    document.getElementById("btn-week").classList.add("btn-selected");
                }
                this.$root.fetchAsteroids(days);
            },
            isMissingData: function (a) {
                return a.close_approach_data.length == 0;                    
            }
        }
    }
</script>

<style scoped>
    table{
        margin: auto;
        text-align: center;
        animation: fade-in 1s;
        transition: 1s ease-in;
    }
    table th{
        padding: 2vw;
        padding-bottom: 1em;
        font-weight: 100;
        font-size: 5vw;
        transition: 1s ease;
    }
    table td{
        animation: fade-in 1s;
        transition: 1s ease-in;
        padding: 1em 0.5em;
        font-size: 3.5vw;
    }
    table tr:first-child{
        color: #18AB39;
    }
    .NEO-container{
        text-align: center;
    }
    .date-btn{
        margin: 50px 20px;
    }
    .loading-text{
        margin: auto;
        text-align: center;
    }
    .NEO-container{
        margin: 100px 0px;
    }
    @media only screen and (min-width: 500px) {
        .date-btn{
        margin: 30px;
        }
        table th{
            font-size: 1.9em;
        }
        table td{
            font-size: 1em;
        }
    }
</style>