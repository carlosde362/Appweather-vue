<template>
  <div id="app">
    <div class="contenedor">
      <div class="buscador">
        <input
          type="text"
          id="ciudadID"
          class="form-buscar"
          v-model="ciudad"
          placeholder="Nombre de la ciudad..."
          @keyup.enter="fcomprobar"
        />
      </div>
      <div class="vertiempo" v-if="this.localizacion != null">
        <h1>
          {{ this.localizacion }}
        </h1>
        <h2>
          {{ this.temperatura }}
          {{ this.estadoActual }}
        </h2>
        <h2>{{ this.humedad }}</h2>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data: function () {
    return {
      ciudad: "",
      openweather: this.fcrearObjeto(),
      tiempoActual: undefined,
      localizacion: null,
      temperatura: null,
      estadoActual: null,
      humedad: null,
    };
  },
  methods: {
    fcomprobar() {
      const ciudad = this.ciudad;
      const ExpreCiudad = /^([a-z]+|[a-z]+\s[a-z+])+$/i;
      if (ExpreCiudad.test(ciudad)) {
        this.fverTiempo(ciudad);
      }
    },
    fverTiempo(ciudad) {
      this.openweather.setCity(ciudad);
      this.openweather.getAllWeather((err, inf) => this.fmostrar(inf));
    },
    fmostrar(datosTiempo) {
      console.log(datosTiempo);
      this.localizacion = datosTiempo.name + ", " + datosTiempo.sys.country;
      this.temperatura = Math.round(datosTiempo.main.temp) + "ºC";
      this.estadoActual = datosTiempo.weather[0].description;
      this.humedad = datosTiempo.main.humidity + "% humedad";
      if (datosTiempo.main.temp >= 20) {
        document.getElementById("app").style.backgroundImage =
          "url('./assets/hot.jpg')";
      }
    },
    fcrearObjeto() {
      const weather = require("openweather-apis");
      weather.setAPPID("e2cd17e960a8e30856d9602c73d23626");
      weather.setLang("es");
      weather.setUnits("metric");
      return weather;
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Open+Sans:wght@700&display=swap");
body {
  background-image: url("./assets/green.jpg");
  width: 90%;
  margin: auto;
}

.contenedor {
  width: 100%;
  height: 100%;
  display: block;
}

body.cambiarFondo {
  background-image: url("./assets/hot.jpg");
}

.buscador {
  padding: 20px;
  margin-top: 5%;
  display: flex;
  justify-content: center;
  align-content: center;
  align-items: center;
}

.form-buscar {
  padding: 20px;
  font-size: 200%;
  border: none;
  outline: none;
  background-color: rgba(255, 255, 255, 0.5);
  border-top-left-radius: 20px;
  border-bottom-right-radius: 20px;
  transition: 0.5s;
}

.form-buscar:focus {
  background-color: rgba(255, 255, 255, 0.75);
  border-top-right-radius: 20px;
  border-bottom-left-radius: 20px;
  border-top-left-radius: 0;
  border-bottom-right-radius: 0;
}

.vertiempo {
  width: max-content;
  margin: auto;
  padding: 20px;
  color: black;
  font-size: 150%;
  font-weight: bold;
  text-align: center;
  font-family: "Open Sans", sans-serif;
  display: flex;
  flex-direction: column;
  background-color: rgba(255, 255, 255, 0.4);
  box-shadow: 10px 10px 10px 1px rgba(0, 0, 0, 0.75);
}

.vertiempo h1 {
  font-style: italic;
}

@media (max-width: 800px) {
  body {
    background-position: center center;
    background-attachment: fixed;
    background-repeat: no-repeat;
  }
}

@media (max-width: 450px) {
  .form-buscar {
    padding: 10px;
    font-size: 150%;
  }
}
</style>
