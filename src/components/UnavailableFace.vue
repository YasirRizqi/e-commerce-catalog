// src/components/UnavailableFace.vue
<template>
  <div class="unavailable-face">
    <div class="face-element"></div>
    <div class="face-element"></div>
    <div class="face-element"></div>
  </div>
</template>

<script>
export default {
  name: 'UnavailableFace',
}
</script>

<style scoped>
.unavailable-face {
  width: 200px;
  height: 200px;
  position: relative;
  background: #ddd;
  border-radius: 50%;
}

.face-element {
  position: absolute;
  background: #999;
}

.face-element:nth-child(1),
.face-element:nth-child(2) {
  width: 30px;
  height: 30px;
  border-radius: 50%;
  top: 60px;
}

.face-element:nth-child(1) {
  left: 50px;
}

.face-element:nth-child(2) {
  right: 50px;
}

.face-element:nth-child(3) {
  width: 100px;
  height: 20px;
  border-radius: 0 0 100px 100px;
  bottom: 50px;
  left: 50%;
  transform: translateX(-50%);
}
</style>
