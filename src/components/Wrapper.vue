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
      <p>Погода в городе {{ sity == "" ? " у вас" : sityName}}</p>
      <div>
        <input type="text" v-model="sity" class="inputValue" placeholder="Введите название города">
        <button v-if="sity != ''" @click="getWeather()">Узнать погоду</button>
        <button disabled v-else class="buttonDis" >Узнать погоду</button>
        <p class="error">{{ error }}</p>

          <!-- <p v-shiw="info != null"> {{ info.main.temp }}</p> -->
        

      </div>
    </div>
</template>

<style>
.error {
  margin-top: 10px;
  color: red;
}
.wrapper {
  text-align: center;
  border-radius: 25px;
  border: solid #000;
  padding: 20px;
  width: 900px;
  height: 500px;
  background: rgb(255, 255, 255);
}
.inputValue {
  margin-top: 30px;
  background: transparent;
  border: 0;
  border-bottom: 2px solid rebeccapurple;
  font-size: 14px;
  padding: 5px;
  outline: none;
}
.inputValue:focus {
  border-bottom: 2px solid rgb(189, 61, 201);
}

.wrapper button {
  margin: 0 0 0 5px;
  background: yellow;
  border: 0;
  width: 120px;
  height: 30px;
  font-size: 15px;
  font-weight: 700;
  color: #000;
  transition: transform 1s ease;
}
.wrapper button:hover {
  transform: scale(1.1);
}
.buttonDis:disabled {
  background: rgba(255, 255, 136, 0.384);
}
</style>

