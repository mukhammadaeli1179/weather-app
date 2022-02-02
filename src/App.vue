<template>
<div class="wrapper">
  <div class="weatherApp">
    <div class="title">Weather App ⛅</div>
    <div class="request">
      <input type="text" placeholder="Enter location" @keyup.enter="fetchData" v-model="query">
      <button @click="fetchData()">Search</button>
    </div>
    <div class="info" v-if=" typeof weather.data != 'undefined'">
      <h1>{{ weather.data.name }}</h1>
      <p>Temperature:  {{ Math.floor(weather.data.main.temp) }}°C</p>
    </div>
  </div>
</div>

</template>

<script>

import axios from 'axios';

export default {
  name: "App",
    data() {
      return {
        appKey: "ab68d5e98086a465ee9e4a4163cbcb7f",
        query: "",
        urlBase: "https://api.openweathermap.org/data/2.5/",
        weather: {}
      }
    },

    methods: {
      fetchData() {
      axios.get(`${this.urlBase}/weather?q=${this.query}&units=metric&appid=${this.appKey}`)
      .then(res => this.weather = res);
      this.query = ""
      }
    }
};
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@100;200;400;500;600;700;800;900&display=swap');

  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Poppins', sans-serif;
  }

  body{
    background-image: url("../public/images/wallpaper.jpg");
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;
    width: 100%;
    height: 100%;
  }

.wrapper{
  width: 100%;
  height: 100vh;
  display: flex;
  align-items: flex-start;
  justify-content: center;
}

.weatherApp{
  max-width: 500px;
  width: 100%;
  padding: 20px;
}

.title{
  font-size: 42px;
  text-align: center;
  color: #fff;
}

.request{
  margin-top: 30px;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-wrap: nowrap;
}

input{
  width: 70%;
  height: 100%;
  outline: none;
  padding: 8px 15px;
  margin-right: 5px;
  border: 2px solid #fff;
  border-radius: 5px;
  background: none;
  color: #fff;
  font-size: 16px;
}

input::placeholder{
  color: #fff;
}

button{
  width: 30%;
  height: 100%;
  padding: 8px 15px;
  border: 2px solid #fff;
  border-radius: 5px;
  background: #f8fafc;
  color: #3498db;
  cursor: pointer;
  font-size: 16px;
}

button:hover{
  background: none;
  color: #fff;
  border: 2px solid #fff;
}

.info{
  margin-top: 20px;
  width: 100%;
  height: 100%;
}

h1{
  font-size: 34px;
  font-weight: 600;
  color: #fff;
}

p{
  margin-top: 5px;
  font-size: 22px;
  color: #fff;
}

</style>
