<template>
  <div class="loader">
    <div v-for="index in 9" :key="index" class="square" :id="'sq' + index"></div>
  </div>
</template>

<style scoped lang="scss">
@keyframes fade {
  from {
    opacity: 0;
  }

  to {
    opacity: 1;
  }
}

.loader {
  position: relative;
}

.square {
  background: #ddd;
  width: 10px;
  height: 10px;
  position: absolute;
  top: 50%;
  left: 50%;
  margin-top: -5px;
  margin-left: -5px;
  border-radius: 4px;
}

#sq1 {
  margin-top: -25px;
  margin-left: -25px;
  animation: fade 675ms ease-in-out 0s infinite alternate;
}

#sq2 {
  margin-top: -25px;
  animation: fade 675ms ease-in-out 75ms infinite alternate;
}

#sq3 {
  margin-top: -25px;
  margin-left: 15px;
  animation: fade 675ms ease-in-out 150ms infinite;
}

#sq4 {
  margin-left: -25px;
  animation: fade 675ms ease-in-out 225ms infinite;
}

#sq5 {
  animation: fade 675ms ease-in-out 300ms infinite;
}

#sq6 {
  margin-left: 15px;
  animation: fade 675ms ease-in-out 375ms infinite;
}

#sq7 {
  margin-top: 15px;
  margin-left: -25px;
  animation: fade 675ms ease-in-out 450ms infinite;
}

#sq8 {
  margin-top: 15px;
  animation: fade 675ms ease-in-out 525ms infinite;
}

#sq9 {
  margin-top: 15px;
  margin-left: 15px;
  animation: fade 675ms ease-in-out 600ms infinite;
}
</style>
