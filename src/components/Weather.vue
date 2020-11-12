<template>
<div id="main">
    <div class="row">
        <div class="col-6 col-md-4 col-sm-12 col-xs-12" v-for="weather in arrWeather" :key="weather.id">
            <div class="card p-4">
                <div class="d-flex">
                    <h4 class="flex-grow-1">{{ weather.name }}</h4>
                </div>
                <div class="d-flex flex-column temp mt-5 mb-3">
                    <h1 class="mb-0 font-weight-bold" id="heading"> {{ weather.main.temp }}° C </h1> <span class="small grey">{{ weather.weather[0].description }}</span>
                </div>
                <div class="d-flex">
                    <div class="temp-details flex-grow-1">
                        <p class="my-1"> <img src="https://i.imgur.com/B9kqOzp.png" height="17px"> <span> {{ weather.wind.speed }} km/h </span> </p>
                        <p class="my-1"> <i class="fa fa-tint mr-2" aria-hidden="true"></i> <span> {{ weather.main.humidity }}% </span> </p>
                        <p class="my-1"> <img src="https://i.imgur.com/wGSJ8C5.png" height="17px"> <span> 0.2h </span> </p>
                    </div>
                    <div> <img :src="weather.url" width="100px"> </div>
                </div>
            </div>
        </div>
    </div>
    <button id="btn" v-on:click="getWeather()">Lấy thông tin thời tiết</button>
</div>
</template>

<script>
export default {
    data() {
     return {
       weather: null,
        server_url: "http://api.openweathermap.org/data/2.5/weather",
        location_ids: ["1581129","1559969","1559970","1559971","1559972",
        "1562414","1562548","1562693","1562798","1562820",
        "1563241","1563281","1563287","1563926","1564676","1565022",
        "1565033","1565088","1565593","1565654","1565681","1566053",
        "1566083","1566165","1566338","1566557","1567621"],
        api_key: "d6477696b63c2e661af64eead58c11d9",
        arrWeather: [],
        active: true
     }
   },
   methods: {
    async randomNumber() {  
        return Math.floor(Math.random() * 20) + 1; 
    },
    async getWeather() {
        this.arrWeather = [];
        this.active = false;
        const index = await this.randomNumber();
        for(let i = 1; i <= 3;i++){
            var url = this.server_url + `?id=${this.location_ids[index+i]}&units=metric&appid=${this.api_key}`;
            var response = await fetch(url);
            this.weather = await response.json();
            if(this.weather.weather[0].description === 'clear sky'){
                this.weather.url = "https://img.icons8.com/emoji/96/000000/sun-emoji.png";
            }
            else if(this.weather.weather[0].description === 'scattered clouds'){
                this.weather.url = "https://img.icons8.com/office/80/000000/partly-cloudy-day.png"
            }
            else if(this.weather.weather[0].description === 'few clouds'){
                this.weather.url = "https://img.icons8.com/color/50/000000/wind.png"
            }
            else if(this.weather.weather[0].description === 'warm'){
                this.weather.url = "https://img.icons8.com/emoji/96/000000/sun-emoji.png"
            }
            else{
                this.weather.url = "https://i.imgur.com/Qw7npIg.png"
            }
            this.arrWeather.push(this.weather)
        }
    }
   },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Marcellus&display=swap');
@import url('https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css');
@import url('https://maxcdn.bootstrapcdn.com/bootstrap/4.4.1/css/bootstrap.min.css');


#main{
    width: 100%;
    height: 100%;
    position: relative;
}

.row{
    position: absolute;
    top: 25%;
    left: 20%;
}

.p-4{
    border-radius: 50px;
}


.card {
    background-color: #ffffff;
    color: #2a2b3a;
    font-family: 'Marcellus', serif;
    margin-top: 16px;
    height: 400px;
}

#heading {
    font-size: 55px;
    color: #2b304d
}

.temp {
    place-items: center
}

.temp-details>p>span,
.grey {
    color: #171a20;
    font-size: 12px
}

.fa {
    color: #a5a5b1
}

*:focus {
    outline: none
}

#btn{
    position: absolute;
    height: 50px;
    width: 180px;
    top: 20%;
    left: 50%;
    border-radius: 10px;
}

</style>
