<template>
  <div id="app">
    <div class="mb-3 group">
      <label for="formFile" class="form-label">Peso</label>
      <input
        class="form-control"
        type="number"
        id="formFile"
        min="0"
        v-model="weight"
      />
    </div>
    <div class="mb-3 group">
      <label for="formFile" class="form-label">Altura</label>
      <input
        class="form-control input"
        type="number"
        id="formFile"
        min="0"
        v-model="height"
      />
    </div>
    <button type="button" class="btn btn-primary" @click="calc">
      Calcular
    </button>
    <div v-bind:class="type" role="alert">{{ message }}</div>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      height: 0,
      weight: 0,
      message: "",
      type: "",
    };
  },

  methods: {
    calc() {
      const imc = parseFloat((this.weight / this.height ** 2) * 10000).toFixed(
        2
      );

      if (this.height <= 0 || this.weight <= 0) {
        this.message =
          "A altura e o peso devem ser preenchidos e maior que zero";
        this.type = "alert alert-info";
      } else if (imc < 18.5) {
        this.message = "IMC: " + imc + " - Abaixo do peso";
        this.type = "alert alert-danger";
      } else if (imc === 18.5 || imc <= 24.9) {
        this.message = "IMC: " + imc + " - Peso normal";
        this.type = "alert alert-primary";
      } else if (imc === 25 || imc <= 29) {
        this.message = "IMC: " + imc + " - Sobrepeso";
        this.type = "alert alert-warning";
      } else if (imc === 30 || imc <= 34.9) {
        this.message = "IMC: " + imc + " - Obesidade grau 1";
        this.type = "alert alert-danger";
      } else if (imc === 35 || imc <= 39.9) {
        this.message = "IMC: " + imc + " - Obesidade grau 2";
        this.type = "alert alert-danger";
      } else {
        this.message = "IMC: " + imc + " - Obesidade grau 3";
        this.type = "alert alert-danger";
      }
    },
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.group {
  width: 40%;
  margin: 40px auto;
}

.btn {
  margin: 20px auto;
}

.alert {
  width: 40%;
  margin: 5px auto;
}
</style>
