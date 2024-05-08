<template>
  <div class="fuel-calculator">
    <h2>Fuel Calculator</h2>
    <div class="input-group">
      <label for="distance">Distance (km):</label>
      <input type="number" id="distance" v-model="distance" />
    </div>
    <div class="input-group">
      <label for="fuel-consumption">Average Fuel Consumption (L/100km):</label>
      <input type="number" id="fuel-consumption" v-model="fuelConsumption" />
    </div>
    <div class="input-group">
      <label for="fuel-price">Fuel Price per Liter:</label>
      <input type="number" id="fuel-price" v-model="fuelPrice" />
    </div>
    <button @click="calculatePrice">Calculate</button>
    <div class="result" v-if="price !== null">
      <p>Price for the needed fuel: {{ price.toFixed(2) }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      distance: 0,
      fuelConsumption: 0,
      fuelPrice: 0,
      price: null
    };
  },
  methods: {
    calculatePrice() {
      const fuelNeeded = (this.distance / 100) * this.fuelConsumption;
      this.price = fuelNeeded * this.fuelPrice;
    }
  }
};
</script>

<style scoped lang="scss">
@import "../assets/css/main.css";

.fuel-calculator {
  color: var(celadon);
  max-width: 500px;
  margin: 0 auto;
  padding: 20px;
}

.input-group {
  margin-bottom: 10px;
}

label {
  display: block;
  margin-bottom: 5px;
}

input[type="number"] {
  width: 100%;
  padding: 5px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

button {
  display: block;
  margin-top: 10px;
  padding: 10px 20px;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.result {
  margin-top: 20px;
  padding: 10px;
  background-color: #f0f0f0;
}
</style>