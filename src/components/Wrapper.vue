<script>
  import axios from 'axios'
  export default {
    data() {
      return {
        sity : "",
        error: "",
        info: null
      }
    },
    computed: {
      sityName() {
        return "<" + this.sity + ">"
      },
      showTemp() {
        return "Температура " + this.info.main.temp
      },
      showFeelsLike () {
        return "Ощущается как " + this.info.main.feels_like
      },
      showTempMin () {
        return "Минимальная температура " + this.info.main.temp_min
      },
      showTempMax () {
        return "Максимальная температура " + this.info.main.temp_max
      }
    },
    methods: {
      getWeather() {
        if(this.sity.trim().length <  2) {
          this.error = "Введите верные данные"
          return false
        }
        else {
          this.error = ""

          axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.sity}&units=metric&appid=d82a7a8edaff5ea30b2af3e79bd44604`)
                .then(res => (this.info=res.data))
        }
      } 
    }
  }
</script>

<template>
    <div class="wrapper">
      <h1>WeatherWEB</h1>
      <h2>Погода в городе {{ sity == "" ? " у вас" : sityName}}</h2>
      <div>
        <input type="text" v-model="sity" class="inputValue" placeholder="Введите название города">
        <button v-if="sity != ''" @click="getWeather()">Узнать погоду</button>
        <button disabled v-else class="buttonDis" >я жду данные</button>
        <p class="error">{{ error }}</p>

        <div v-if="info != null" class="textData">
          <p > {{ showTemp }}</p>
          <p > {{ showFeelsLike }}</p>
          <p > {{ showTempMin }}</p>
          <p > {{ showTempMax }}</p>
        </div>

      </div>
    </div>
</template>

<style>
.wrapper h1 {
  font-size: 120px;
}
.wrapper h2 {
  font-size: 30px;
}
.error {
  margin: 10px 0;
  color: #8E8D8A;
  font-size: 20px;
  font-weight: 700;
}
.wrapper {
  text-align: center;
  border-radius: 25px;
  border: solid #8E8D8A;
  padding: 20px;
  width: 900px;
  height: 500px;
  background: #EAE7DC;
  color: #E85A4F;
}
.inputValue {
  margin-top: 30px;
  background: transparent;
  border: 0;
  border-bottom: 2px solid #D8C3A5;
  font-size: 20px;
  padding: 5px;
  outline: none;
  color: #E98074;
}
.inputValue:focus {
  border-bottom: 2px solid #8E8D8A;
}

.wrapper button {
  margin: 0 0 0 5px;
  background: #EAE7DC;
  border-radius: 10px;
  border: #8E8D8A 2px solid;
  width: 128px;
  height: 30px;
  font-size: 15px;
  font-weight: 700;
  color: #E98074;
  transition: transform 1s ease;
}
.wrapper button:hover {
  transform: scale(1.1);
}
.buttonDis:disabled {
  background: #D8C3A5;
}
.textData {
  font-size: 30px;
}
</style>

