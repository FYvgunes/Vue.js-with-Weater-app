<template>
  <div id="app">
<main>
  <div class="searc-box">
    <input
      type="text"
      class="searc-bar"
      placeholder="Öğrenmek istediğin bilgileri giriniz."
      v-model="query"
      @keypress="fetchWeather"
    >

  </div>

  <div class="weater-wrap" v-if="typeof weather.main != 'undefined'">
    <div class="location-box">
      <div class="location">{{weather.name }}, {{weather.sys.country}}</div>
      <div class="date">{{databuild()}}</div>
    </div>

  </div>

  <div class="weater-box">
    <div class="temp"> {{Math.round(weather.main.temp)}}°C</div>
    <div class="weater">{{weather.weather[0].main}}</div>
  </div>

</main>
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      api_key: "5d9e156fb8a5307802470209fa882947",
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {},


    }
  },
  methods: {
    fetchWeather(e) {
      if (e.key == "Enter") {
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
          .then(res => {
            return res.json();

          }).then(this.setResults);
      }
    },
    setResults(results){
      console.log(this.weather);
      this.weather = results;
    },
    databuild(){
      let d = new Data();
      let mounts = ["Ocak","Şubat","Mart","Nisan","Mayıs","Hazıran","Temmuz","Ağustos","Eylül","Ekim","Kasım","Aralık"];
      let days = ["Pazartesi","Salı","Çarşamba","Perşembe","Cuma","Cumartesi","Pazar"];

      let day = days[d.getDay()];
      let date = d.getDate();
      let mount= mounts[d.getMonth()];
      let year = d.getFullYear();

      return `${date} ${day} ${mount} ${year}`;

   }

  }
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing:border-box;
}
body{
  font-family: 'montserrat' ,sans-serif;
}
#app{
  background-image: url("./assets/cold.jpg");
  background-size: cover;
  background-position:center;
  transition: 0.4s;
}
main{
  min-height: 100vh;
  padding: 75px;
  background-image: linear-gradient(to bottom, rgba(0,0,0,0.25), rgba(0,0,0,0.85));

}
.searc-box{
  width: 100%;
  margin-bottom: 30px;
}
.searc-box .searc-bar{
  display: block;
  width: 100%;
  padding: 15px;
  color:#313131;
  font-size: 17px;
  appearance: none;
  outline: none;
  border: none;
  background-color: rgba(255,255,255,0.5);
  border-radius: 0px 15px 0 15px;
  transition: 0.4s;
}
.searc-box .searc-bar:focus{
  background-color: rgba(255,255,255,0.75);
}
.location-box .location{
  color: #fff;
  font-size: 32px;
  text-align: center;
  text-shadow: 1px 3px rgba(0,0,0,0.25);
}
.location-box .date{
  color: #fff;
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
}
.weater-box{
  text-align: center;

}
.weater-box .temp{
  display: inline-block;
  padding: 10px 25px;
  color: #fff;
  font-weight: 900;
  font-size: 100px;
  text-shadow: 3px 6px rgba(0,0,0,0.25);
  background-color: rgba(255,255,255,0.25);
  border-radius: 16px;
  margin: 30px 0px;
  box-shadow: 3px 6px rgba(0,0,0,0.25);
}
.weater-box .weater{
  color: #ffffff;
  font-size: 40px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0,0,0,0.25);
}


</style>
