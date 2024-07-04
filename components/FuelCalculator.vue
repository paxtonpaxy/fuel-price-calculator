<script setup>
  import { ref } from 'vue';
  // variables
  const distance = ref('');
  const fuelConsumption = ref('');
  const fuelPrice = ref('');
  const price = ref(null);

  // validation for the input fields
  const distanceHasvlue = ref(false);
  const distanceIsValid = ref(true);

  const fuelConsumptionHasValue = ref(false);
  const fuelConsumptionIsValid = ref(true);

  const fuelPriceHasValue = ref(false);
  const fuelPriceIsValid = ref(true);

  // regex for the input fields
  const regex = /^[0-9]*\.?[0-9]*$/;

  // METHODS
  function calculatePrice() {
    const fuelNeeded = (distance.value / 100) * fuelConsumption.value;
    price.value = fuelNeeded * fuelPrice.value;
  }
  // validate the input fields and check if they have a value for the border
  function validateInput() {
    if (distance.value !== '' && !regex.test(distance.value)) {
      distanceIsValid.value = false;
    } else {
      distanceIsValid.value = true;
    }

    if (fuelConsumption.value !== '' && !regex.test(fuelConsumption.value)) {
      fuelConsumptionIsValid.value = false;
    } else {
      fuelConsumptionIsValid.value = true;
    }

    if (fuelPrice.value !== '' && !regex.test(fuelPrice.value)) {
      fuelPriceIsValid.value = false;
    } else {
      fuelPriceIsValid.value = true;
    }

    checkInput();
  }
  // check if the input fields have a value for the label placement
  function checkInput() {
    if (distance.value !== '') {
      distanceHasvlue.value = true;
    } else {
      distanceHasvlue.value = false;
    }

    if (fuelConsumption.value !== '') {
      fuelConsumptionHasValue.value = true;
    } else {
      fuelConsumptionHasValue.value = false;
    }

    if (fuelPrice.value !== '') {
      fuelPriceHasValue.value = true;
    } else {
      fuelPriceHasValue.value = false;
    }
  }
</script>

<template>
  <div class="fuel-calculator">
    <form @submit.prevent>
      <div class="input-and-label">
        <input
          id="distance"
          class="input-and-label__input"
          :class="{
            'invalid-border': !distanceIsValid,
            'input-and-label__input--has-value': distanceHasvlue
          }"
          type="text"
          required
          @input="validateInput"
          v-model="distance" 
        />
        <label for="distance">
          Distance in (km)
        </label>
      </div>
      <div class="input-and-label">
        <input
          id="fuel-consumption"
          class="input-and-label__input"
          :class="{
            'invalid-border': !fuelConsumptionIsValid,
            'input-and-label__input--has-value': fuelConsumptionHasValue
          }"
          type="text" 
          required
          @input="validateInput"
          v-model="fuelConsumption" 
        />
        <label for="fuel-consumption">
          Consumption (L/100km)
        </label>
      </div>
      <div class="input-and-label">
        <input
          id="fuel-price"
          class="input-and-label__input"
          :class="{
            'invalid-border': !fuelPriceIsValid,
            'input-and-label__input--has-value': fuelPriceHasValue
          }"
          type="text" 
          required
          @input="validateInput"
          v-model="fuelPrice" 
        />
        <label for="fuel-price">
          Price per Liter
        </label>
      </div>
      <button @click="calculatePrice">Calculate</button>
    </form>
    <div class="result" v-if="price !== null">
      <p>Price for the needed fuel: {{ price.toFixed(2) }}</p>
    </div>
  </div>
</template>

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

  form {
    display: flex;
    flex-direction: column;
    gap: 1.5rem;
  }

  .input-and-label {
    position: relative;
    width: 100%;

    label {
      left: 0.5rem;
      position: absolute;
      text-transform: uppercase;
      font-size: 0.75rem;
      padding: 0.6rem;
      pointer-events: none;
      color: var(--primary-color);
      transition: all 0.3s ease-in-out;

      @media screen and (min-width: 500px){
        font-size: 1rem;
      }
    }

    &__input {
      width: 100%;
      padding: 0.6rem;
      border: 1px solid var(--primary-color);
      background: var(--dark-color);
      border-radius: 1rem;
      outline: none;
      color: var(--primary-color);
      font-size: 1rem;

      &--has-value + label {
        transform: translateX(5rem) translateY(-0.8rem);
        background: var(--primary-color);
        color: var(--dark-color);
        border-radius: 0.25rem;
        font-size: 0.7rem;
        padding: 0.2rem 0.4rem;

        @media screen and (min-width: 500px){
          transform: translateX(15rem) translateY(-0.8rem);
        }
      }

      &:focus + label {
        transform: translateX(5rem) translateY(-0.8rem);
        background: var(--primary-color);
        color: var(--dark-color);
        border-radius: 0.25rem;
        font-size: 0.7rem;
        padding: 0.2rem 0.4rem;

        @media screen and (min-width: 500px){
          transform: translateX(15rem) translateY(-0.8rem);
        }
      }
    }
  }

  .invalid-border {
    border: 1px solid red;
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
