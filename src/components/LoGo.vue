<script setup></script>
<template>
  <div class="logo-container">
    <div class="logo-shape">
      <div class="logo-inner"></div>
    </div>
  </div>
</template>
<style scoped>
.logo-container {
  width: 50px;
  height: 50px;
  display: flex;
  justify-content: center;
  align-items: center;
  transform: scale(0.6);
}
.logo-shape {
  position: relative;
  width: 100%;
  height: 100%;
  background-color: black;
  border-radius: 100% 75% 100% 0%;
}
.logo-inner {
  position: relative;
  width: 100%;
  height: 50%;
  background-color: rgb(255, 255, 255);
  border-radius: 80% 10% 50% 0%;
  transform: translateY(15px);
}
.logo-inner:after {
  content: '';
  position: absolute;
  top: 5px;
  right: 10px;
  width: 10px;
  height: 10px;
  border-radius: 100%;
  background-color: black;
}
.logo-inner:before {
  content: '';
  position: absolute;
  top: 5px;
  left: 100%;
  width: 12px;
  height: 8px;
  border-top-right-radius: 100%;
  border-bottom-left-radius: 0;
  background-color: black;
}
</style>
