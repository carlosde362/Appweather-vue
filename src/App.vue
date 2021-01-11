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
        />
        <button @click="fconsultar">Consultar</button>
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
    };
  },
  methods: {
    fconsultar() {
      window.alert(this.ciudad);
    },
  },
};
</script>

<style>
body {
  /* background-color: grey; */
  background-image: url("./assets/green.jpg");
  margin: auto;
}
.contenedor {
  width: 100%;
  height: 100%;
  display: block;
}

.buscador {
  padding: 20px;
  border: solid red;
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

.buscador button {
  margin: 10px;
  padding: 15px;
  background-color: #273746;
  color: white;
  border: none;
  outline: none;
  border-radius: 10px;
}

@media (max-width: 800px) {
  body {
    background-position: center center;
    background-attachment: fixed;
    background-repeat: no-repeat;
  }
}
</style>
