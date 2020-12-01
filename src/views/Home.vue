<template>
  <div class="home">
      <main>
          <div class="search-box">
              <input type="text"
                     class="search-bar"
                     placeholder="serach..."
                     v-model="query"
                     />
          </div>
          <div class="search-button-box">
              <input type="button" class="search-button" v-on:click="fetchWeather" value="SEARCH"/>
          </div>
          <div class="weather-wrap">
              <div class="location-box">
                  <div class="location"> {{ this.location }} </div>
                  <div class="date"> {{ this.date }} </div>
              </div>
          </div>

          <div class="weather-box">
              <div class="temp"> {{ this.temp }}°c </div>
              <div class="weather"> {{ this.weather }} </div>
          </div>
      </main>
  </div>
</template>

<script>

export default {
        name: 'Home',
        data() {
            return {
                api_key: '2ebb6e5f7a080bafcd1775a3c73466e1',
                url_base: 'https://api.openweathermap.org/data/2.5/weather?q=',
                query: '',
                location: '',
                date: '',
                temp:'',
                weather: '',
            }
        },
        methods: {
            fetchWeather() {
              fetch(this.url_base + this.query + '&appid=2ebb6e5f7a080bafcd1775a3c73466e1')
                        .then(res => {
                            return res.json();
                        }).then(data => {
                            console.log(data);
                            this.location = data['name'];
                            this.temp = data['main']['temp'];
                            this.weather = data['weather'][0]['description'];
                        });
            }
        }
}
</script>

<style>

    .search-box .search-bar {
        
        width: 95%;
        padding: 15px;
        border: none;
        outline: none;
        /*background: none;*/

        border-radius:0px 16px 0px 16px;
        transition:0.4s;
    }

    .search-button-box .search-button {
        width: 50%;
        margin: 10px;
        padding: 10px;
        border: none;
        border-radius: 16px;
    }


    body {
        font-family: 'montserrat', sans-serif;
    }

    .location-box .location {
        color: #FFF;
        font-size: 32px;
        font-weight: 500;
        text-align: center;
        text-shadow: 1px 1px rgba(0,0,0,0.25);
    }

    .location-box .date {
        color: #FFF;
        font-size: 20px;
        font-weight: 300;
        font-style:italic;
        text-align: center;
    }

    .weather-box {
        text-align:center;
    }

    .weather-box .temp {
        display:inline-block;
        padding:10px 25px;
        color:#FFF;
        font-size:100px;
        font-weight:900;

        text-shadow:1px 2px rgba(0,0,0,0.25);
        background-color:rgba(255, 255, 255, 0.25);
        border-radius:16px;
        margin:30px 0px;

        box-shadow:3px 6px rgba(0,0,0,0.25);
    }

        .weather-box .weather {
            padding: 10px 25px;
            color: #FFF;
            font-size: 100px;
            font-weight: 900;
            text-shadow: 1px 2px rgba(0,0,0,0.25);
        }

</style>