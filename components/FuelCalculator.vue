<script setup>
import { ref } from 'vue';

const consumption = ref(null);
const distance = ref(null);
const price = ref(null);
const totalCost = ref(null);
const loading = ref(false);

const calculate = () => {
  loading.value = true;
  setTimeout(() => {
    if (consumption.value && distance.value && price.value) {
      totalCost.value = ((distance.value / 100) * consumption.value * price.value).toFixed(2);
      loading.value = false;
    } else {
      totalCost.value = null;
    }
  }, 1000);
}

const clearInputFields = () => {
  consumption.value = null;
  distance.value = null;
  price.value = null;
};

const inputValidation = (e) => {
  const input = e.target;
  if (input.value.length > 4) {
    input.value = input.value.slice(0, 5);
  }  
};

const preventInvalidChars = (e) => {
  const invalidChars = ["e", "E", "+", "-"];
  if (invalidChars.includes(e.key)) {
    e.preventDefault();
  }
};

const isFormValid = computed(() => {
  return consumption.value && distance.value && price.value;
});
</script>

<template>
  <div class="fuel-calculator">
    <div class="fuel-calculator__description">
      <h2>Fuel cost calculator</h2>
    </div>
    <form class="fuel-calculator__form" @submit.prevent="calculate">
      <div class="input-wrapper" data-placeholder="l / km">
        <input
          type="number"
          @input="inputValidation"
          @keydown="preventInvalidChars"
          required
          v-model="consumption"
          placeholder="Liters per kilometer ~ 7.5"
          step="0.01"
        >
      </div>
      <div class="input-wrapper" data-placeholder="km">
        <input
          type="number"
          required
          @keydown="preventInvalidChars"
          v-model="distance"
          placeholder="Distance ~ 450"
        >
      </div>
      <div class="input-wrapper" data-placeholder="€">
        <input
          type="number"
          required
          @keydown="preventInvalidChars"
          v-model="price"
          step="0.01"
          placeholder="Fuel price per liter ~ 1.9"
        >
      </div>
      <div class="fuel-calculator__description">
        <p>
          Calculate how much will fuel cost you for your trip. Make sure to enter all the fields, and press calculate please...
        </p>
    </div>
      
      <button class="fuel-calculator__form--button" type="submit" :disabled="!isFormValid">
        Calculate
      </button>
    </form>
    <div v-if="loading" class="fuel-calculator__output loading">
      <Loader />
    </div>
    <div v-else-if="totalCost !== null" class="fuel-calculator__output">
      <div>
        {{ totalCost }} <span> € </span>
      </div>
      <div>
        <button @click="clearInputFields" class="fuel-calculator__output--button"> Clear </button>
      </div>
    </div>
    <div v-else class="fuel-calculator__output empty">
      <p>
        Enter the numbers above please...
      </p>
    </div>
  </div>
</template>

<style scoped lang="scss">
@keyframes fadeInLeftToRight {
  0% {
    opacity: 0;
    transform: translateX(-30px);
  }
  100% {
    opacity: 1;
    transform: translateX(0);
  }
}

.fuel-calculator {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 2rem;
  gap: 3rem;
  width: 80dvw;

  &__description {
    display: flex;
    flex-direction: column;
    gap: 1rem;
    word-break: break-word;
    color: #e4e4e4;
    width: 100%;

    p {
      color: #a5a5a5;
    }
  }
  
  &__form {
    display: flex;
    flex-direction: column;
    gap: 1rem;
    width: 100%;

    .input-wrapper {
      position: relative;
      height: auto;
      width: auto;

      &:has(input:focus)::after,
      &:has(input:required:valid)::after {
        opacity: 1;
        animation: fadeInLeftToRight 0.5s ease-in-out forwards;
        color: #a5a5a5;
      }

      &::after {
        content: attr(data-placeholder);
        position: absolute;
        width: fit-content;
        top: 12px;
        right: 16px;
        color: #a5a5a5;
        transition: all 200ms;
        pointer-events: none;
        opacity: 0;
      }

      input {
        &::-webkit-outer-spin-button,
        &::-webkit-inner-spin-button {
          -webkit-appearance: none;
          margin: 0;
        }

        outline: none;
        width: 100%;
        height: auto;
        padding: 12px 16px;
        border-radius: 8px;
        color: #fff;
        font-family: inherit;
        background-color: transparent;
        border: 1px solid #555555;
        transition: all 200ms ease-in-out;

        &:hover {
          border: 1px solid #e4e4e4;
        }

        &:valid {
          border: 1px solid #e4e4e4;
        }
      }
    }

    &--button {
      width: 100%;
      padding: 12px 16px;
      border-radius: 8px;
      color: #fff;
      font-family: inherit;
      background-color: transparent;
      border: 1px solid #e4e4e4;
      transition: all 200ms ease-in-out;


      &:hover:not(:disabled) {
        cursor: pointer;
        background: linear-gradient(45deg, #202020, #252525);
        border: 1px solid #fff;
      }

      &:disabled {
        opacity: 0.5;
      }
    }
  }

  .loading {
    min-height: 100px;
  }

  &__output {
    display: flex;
    justify-content: space-between;
    width: 100%;
    padding: 12px 16px;
    border-radius: 8px;
    color: #fff;
    font-family: inherit;
    background-color: transparent;
    border: 1px solid #e4e4e4;

    &--button {
      cursor: pointer;
      font-size: 16px;
      letter-spacing: 1px;
      color: #e4e4e4;
      text-decoration: underline;
      text-underline-position: under;
      border: none;
      background: transparent;
    }

    p {
      font-size: 14px;
    }
  }

  &__output.empty {
    border: 1px solid #555555;
    color: #555555;
  }

  &__output.loading {
    border: 1px solid #555555;
    display: flex;
    justify-content: center;
  }
}

@media  screen and (min-width: 768px) {
  .fuel-calculator {
    margin-top: 4rem;
    margin-bottom: 4rem;
    max-width: 768px;
    border: 1px solid #555555;
    border-radius: 0.4rem;
    padding: 2rem;
  }
}
</style>
