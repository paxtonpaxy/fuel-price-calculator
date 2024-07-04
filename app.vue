<!-- <script setup>
  function themeToggle() {
    const isLight = document.body.getAttribute('theme') === 'light';
    isLight ? document.body.removeAttribute('theme') : document.body.setAttribute('theme', 'light');
  }
</script> -->

<template>
  <div class="h-app">
    <h1>Fuel Calculator</h1>
    <FuelCalculator />
  </div>
</template>

<style lang="scss">
@import url('./assets/css/main.css');
  body {
    height: 100dvh;
    background: var(--dark-color);
  }

  .h-app {
    display: flex;
    flex-direction: column;
    align-items: center;

    h1 {
      color: #f0f0f0;
      font-size: 2rem;
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
  }
</style>
