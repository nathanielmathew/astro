<template>
    <div class="sunrise-container">
        <img src="../assets/sunrise.png" />
        <h1 v-cloak v-if="time<sunset">Sunset at {{(sunset.toLocaleTimeString())}}</h1>
        <h1 v-cloak v-else>Sunrise at <br /> <h2 class="sun-time">{{(sunrise.toLocaleTimeString())}}</h2></h1>
    </div>
</template>

<script>
    export default {
        props: ['sunrise', 'sunset'],
        data: function() {
            return {            
                day: true,
                time: new Date(),
            }
        },
        
        methods: {
            
        }
    }
</script>

<style scoped>
    .sun-time{
        margin-top: 0.2em;
    }
    .sunrise-container{
        margin: 250px 0px;
        text-align: center;
    }
    img{
        max-width: 100%;
    }
    .sunrise-container h1{
        font-size: 3em;
        line-height: 150%;
    }
</style>