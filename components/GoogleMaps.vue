<script setup>
import { ref } from 'vue';

const showMap = ref(false); // Initially, the map is not shown
</script>

<template>
  <div class="google-maps">
    <button
      class="map-button"
      :class="showMap ? 'map-button-hide' : 'map-button-show'" 
      @click="showMap = !showMap">
      {{ showMap ? 'Hide' : 'Show' }} Map
    </button>
    <div id="map" v-show="showMap">
      <iframe 
        src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d39551.89317812352!2d5.276979213213893!3d51.71486467550499!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x47c6ee37ad3edd37%3A0x400de5a8d1e7c50!2s's-Hertogenbosch!5e0!3m2!1sen!2snl!4v1720105238746!5m2!1sen!2snl" 
        style="border:0; border-radius:1rem;" 
        allowfullscreen="" 
        loading="lazy" 
        referrerpolicy="no-referrer-when-downgrade">
      </iframe>
    </div>
  </div>
</template>

<style lang="scss" scoped>
@import "../assets/css/main.css";

  .google-maps {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 1rem;
    margin-top: 2rem;
    height: 100%;

    @media screen and (min-width: 500px){
      iframe {
        width: 500px;
        height: 400px;
      }
    }
  }

  .map-button {
    min-width: 105px;
    display: block;
    margin-top: auto;
    padding: 10px 20px;
    color: #fff;
    border: none;
    border-radius: 4px;
    cursor: pointer;

    &-show {
      background-color: var(--primary-color);
    }

    &-hide {
      background-color: var(--danger-color);
    }
  }
</style>
