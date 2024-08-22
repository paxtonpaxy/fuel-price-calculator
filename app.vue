<!-- <script setup>
  function themeToggle() {
    const isLight = document.body.getAttribute('theme') === 'light';
    isLight ? document.body.removeAttribute('theme') : document.body.setAttribute('theme', 'light');
  }
</script> -->

<template>
  <div class="h-app">
    <h1>Fuel Cost Calculator</h1>
    <FuelCalculator />
    <GoogleMaps />
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
    justify-content: center;
    
    @media screen and (max-width: 500px){
      padding: 0 1rem;
    }

    h1 {
      color: #7e7e7ea9;
      font-size: 2rem;
      margin: 2rem 0;
    }
  }
</style>
