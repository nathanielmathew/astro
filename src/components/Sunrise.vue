<template>
    <div class="sunrise-container">
        <h1 v-cloak v-if="time<sunset">Sunset at {{(sunset.toLocaleTimeString())}}</h1>
        <h1 v-cloak v-else>Sunrise at <br /> {{(sunrise.toLocaleTimeString())}}</h1>
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
    .sunrise-container{
        margin: 250px 0px;
        text-align: center;
    }
    .sunrise-container h1{
        font-size: 3em;
        line-height: 150%;
    }
</style>