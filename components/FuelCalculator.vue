<script setup>
import { ref } from 'vue';

const consumption = ref(null);
const distance = ref(null);
const price = ref(null);
const totalCost = ref(null)

const calculate = () => {
  if (consumption.value && distance.value && price.value) {
    totalCost.value = (distance.value / 100) * consumption.value * price.value;
  } else {
    totalCost.value = null;
  }
}

const isFormValid = computed(() => {
  return consumption.value && distance.value && price.value;
});
</script>

<template>
  <div class="fuel-calculator">
    <div class="fuel-calculator__description">
      <h3>Calculate fuel cost</h3>
      <p>
        Calculate how much it will cost you for you trip you are planning to take. Make sure to enter all the fields, and press calculate...
      </p>
    </div>
    <form class="fuel-calculator__form" @submit.prevent="calculate">
      <div class="input-wrapper" data-placeholder="L / km">
        <input
          type="number"
          required
          v-model="consumption"
          placeholder="Liters per kilometer"
          step="0.01"
        >
      </div>
      <div class="input-wrapper" data-placeholder="km">
        <input
          type="number"
          required
          v-model="distance"
          placeholder="Distance"
        >
      </div>
      <div class="input-wrapper" data-placeholder="€">
        <input
          type="number"
          required
          v-model="price"
          step="0.01"
          placeholder="Fuel price"
        >
      </div>
      
      <button class="fuel-calculator__form--button" type="submit" :disabled="!isFormValid">
        Calculate
      </button>
    </form>
    <div v-if="totalCost !== null" class="fuel-calculator__output">
      {{ totalCost }} 
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
        color: #e4e4e4;
      }

      &::after {
        content: attr(data-placeholder);
        position: absolute;
        width: fit-content;
        top: 12px;
        right: 16px;
        color: #e4e4e4;
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

  &__output {
    width: 100%;
    padding: 12px 16px;
    border-radius: 8px;
    color: #fff;
    font-family: inherit;
    background-color: transparent;
    border: 1px solid #555555;

    p {
      font-size: 14px;
    }
  }

  &__output.empty {
    color: #555555;
  }
}

@media  screen and (min-width: 768px) {
  .fuel-calculator {
    margin-top: 4rem;
    margin-bottom: 4rem;
    max-width: 768px;
    border: 1px solid #555555;
    border-radius: 0.4rem;
    box-shadow: 2px 2px 14px #000000;
    padding: 2rem;
  }
}
</style>
