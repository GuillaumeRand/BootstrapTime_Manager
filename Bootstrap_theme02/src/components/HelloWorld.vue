<template>
        <div class="meteo">
            <select name="ville" id="ville" @change="getville($event.target.value)">
                <option value="Paris">Paris</option>
                <option value="Montpellier">Montpellier</option>
                <option value="Nice">Nice</option>
            </select>
            <h3>Météo Actuelle à {{weather.name}}</h3><br>
            <p>
                Température: {{weather.main.temp}}
            </p>
            <p>
                Date: {{date}}
            </p>
        </div>
</template>


<script>
import  axios from 'axios';
import moment from 'moment';

export default {
    name: 'CurrentWeather',
    data() {
        return{
            weather: null
        }
    },
    methods:{
        async getville(villeselected){
            const response = await axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${villeselected}&units=metric&appid=0bb7874fe4adc7d4ffff87ca6f232f6f`);
            this.weather = response.data;
        }
    },
    created: function() {
      axios
        .get('https://api.openweathermap.org/data/2.5/weather?q=Montpellier&units=metric&appid=0bb7874fe4adc7d4ffff87ca6f232f6f')
        .then(res => {
          this.weather= res.data;
          console.log(this.weather);
        })
    },
    computed: {
        date: function(){
            let date = moment().lang("fr").format("DD MMMM YYYY");
            return date;
        }
    }
}
</script>

<style>
    .meteo{
        text-align:center;
    }
</style>