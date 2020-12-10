<template>
    <div  v-if="moonphase < 0"  class="moon-container">
        <div class="moon-info">
            <h1 class="center">Loading...</h1>
            <p>
                Loading Moon Phase Information...
            </p>
        </div>
        <img src="../assets/moon.png"  class="new-moon-img" />
    </div>

    <div  v-else-if="moonphase == 0"  class="moon-container">
        <div class="moon-info">
            <h1 class="center">NEW MOON</h1>
            <p>
                Stargazing around a new moon is the best time to stargaze as the skies are nice and dark. At these times you will be able to see more stars and have better views through telescopes. This is also the best time to visit dark sky sites. 
            </p>
        </div>
        <img src="../assets/moon.png"  class="new-moon-img" />
    </div>

    <div v-else-if="moonphase < 0.25" class="moon-container">
        <div class="moon-info">
            <h1 class="center">WAXING CRESCENT</h1>
            <p>
               The Waxing Crescent Moon starts as the Moon becomes visible again after the New Moon conjunction.
               A waxing crescent moon shines in the west after sunset. It quickly follows the sun below the western horizon.
            </p>
        </div>
        <img src="../assets/waxing-crescent.png" />
    </div>
    
    <div v-else-if="moonphase == 0.25" class="moon-container">
        <div class="moon-info">
            <h1 class="center">FIRST QUARTER</h1>
            <p>
                First quarter moon means we see half of the moon’s day side (a quarter of the whole moon), and the moon is one quarter of the way through the current orbital cycle. 
                The moon is 90 degrees away from the sun in the sky and is half-illuminated from our point of view.
                The First Quarter Moon rises near the middle of the day and sets around the middle of the night in most areas.
            </p>
        </div>
        <img src="../assets/first-quarter.png" />
    </div>

    <div v-else-if="moonphase < 0.5" class="moon-container">
        <div class="moon-info">
            <h1 class="center">WAXING GIBBOUS</h1>
            <p>
                People often see a waxing gibbous moon in the afternoon, shortly after moonrise, while it’s ascending in the east as the sun is descending in the west. It’s easy to see a waxing gibbous moon in the daytime because, at this phase of the moon, a respectably large fraction of the moon’s dayside faces our way.
            </p>
        </div>
        <img src="../assets/waxing-gibbous.png" />
    </div>

    <div v-else-if="moonphase == 0.5" class="moon-container">
        <div class="moon-info">
            <h1 class="center">FULL MOON</h1>
            <p>
                A Full Moon occurs when Earth is located between the Sun and the Moon. This means that the lunar hemisphere facing Earth – the near side – is completely sunlit and appears as a circular disk. 
                The Moon at its brightest (during a full Moon) can actually be a hindrance to astronomy, because it drowns out the light of the fainter stars; it's like natural light pollution.  
            </p>
        </div>
        <img src="../assets/moon.png" />
    </div>

    <div v-else-if="moonphase < 0.75" class="moon-container">
        <div class="moon-info">
            <h1 class="center">WANING GIBBUOS</h1>
            <p>
                A waning gibbous moon rises later at night and appears in the morning sky.
                A waning gibbous moon can surprise you if you happen to be out late in the evening. It rises eerily some hours after sunset, glowing red like a full moon when it’s near the horizon.
                In the few days after full moon, you’ll often see the waning gibbous moon in the west in early morning, floating against the pale blue sky.
            </p>
        </div>
        <img src="../assets/waning-gibbous.png" />
    </div>

    <div v-else-if="moonphase == 0.75" class="moon-container">
        <div class="moon-info">
            <h1 class="center">LAST QUARTER</h1>
            <p>
                A last quarter moon appears half-lit by sunshine and half-immersed in its own shadow. It rises in the middle of the night, appears at its highest in the sky around dawn, and sets around midday. 
                When you look toward a last quarter moon high in the sky, you’re gazing out approximately along the path of Earth’s orbit, in a forward direction.
            </p>
        </div>
        <img src="../assets/third-quarter.png" />
    </div>
    
    <div v-else class="moon-container">
        <div class="moon-info">
            <h1 class="center">WANING CRESCENT</h1>
            <p>
                During the Waning Crescent Moon phase, the illuminated part of the Moon decreases from the lit-up semicircle at Third Quarter until it disappears from view entirely at New Moon. 
                With some variations, the Waning Crescent Moon rises after midnight and is still up and visible in the morning and day sky before it sets in the afternoon.
            </p>
        </div>
        <img src="../assets/waning-crescent.png" />
    </div>
</template>

<script>
    export default {
        props: ['moonphase'],
        
        methods: {
            
        }
    }
</script>

<style scoped>
    .moon-container img{    
        align-self: center;
    }
    .center{
        text-align: center;
    }
    .moon-info{
        max-width: 400px;
    }
    .moon-info h1{
        font-size: 3.5em;
    }
    .moon-info p{
        font-size: 1.5em;
        text-align: center;
    }
    img{
        max-width: 100%;
    }
    .new-moon-img{
        filter: brightness(0.18);
    }
    
@media only screen and (min-width: 500px) {
    
    .moon-info p{
        font-size: 1.5em;
    }
    .moon-container{
        display: flex;
        justify-content: space-around;
    }
}
</style>