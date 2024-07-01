<template>
  <div class="fuel-calculator">
    <div class="input-group">
      <input 
        type="number" 
        required
        v-model="distance" 
        id="distance"  
      />
      <label for="distance">
        Distance in (km)
      </label>
    </div>
    <div class="input-group">
      <input 
        type="number" 
        required
        v-model="fuelConsumption" 
        id="fuel-consumption"  
      />
      <label for="fuel-consumption">
        Consumption (L/100km)
      </label>
    </div>
    <div class="input-group">
      <input 
        type="number" 
        required
        v-model="fuelPrice" 
        id="fuel-price"  
      />
      <label for="fuel-price">
        Price per Liter
      </label>
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
        distance: Number,
        fuelConsumption: Number,
        fuelPrice: Number,
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
    margin-top: 2rem;
    display: flex;
    flex-direction: column;
    height: 100%;
    width: 100%;
    max-width: 500px;
    color: var(--light-color);
    gap: 2rem;
  }


  .input-group {
    position: relative;
    width: 100%;

    label {
      left: 0.5rem;
      position: absolute;
      text-transform: uppercase;
      font-size: 1rem;
      padding: 0.6rem;
      pointer-events: none;
      color: var(--primary-color);
      transition: all 0.3s ease-in-out;
    }

    input {
      width: 100%;
      padding: 0.6rem;
      border: 1px solid var(--primary-color);
      background: var(--dark-color);
      border-radius: 1rem;
      outline: none;
      color: var(--primary-color);
      font-size: 1rem;

      &:focus + label,
      &:valid + label {
        transform: translateX(15rem) translateY(-0.8rem);
        background: var(--primary-color);
        color: var(--dark-color);
        border-radius: 0.5rem;
        font-size: 0.7rem;
        padding: 0.2rem 0.4rem;
      }
    }
  }

  button {
    display: block;
    margin-top: auto;
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
    color: var(--light-color);
  }
</style>