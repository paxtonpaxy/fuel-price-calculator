<template>
  <div class="google-maps">
    <div id="map">
      <iframe 
        src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d39551.89317812352!2d5.276979213213893!3d51.71486467550499!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x47c6ee37ad3edd37%3A0x400de5a8d1e7c50!2s&#39;s-Hertogenbosch!5e0!3m2!1sen!2snl!4v1720105238746!5m2!1sen!2snl" 
        width="600" 
        height="450" 
        style="
          border:0;
          border-radius:1rem;
        " 
        allowfullscreen="" 
        loading="lazy" 
        referrerpolicy="no-referrer-when-downgrade">
      </iframe>
    </div>
  </div>
</template>

<script>
export default {

}
</script>

<style>
@import "../assets/css/main.css";

.google-maps {
  margin-top: 2rem;
  height: 100%;
}

</style>
