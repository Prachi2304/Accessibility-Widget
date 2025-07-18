<template>
  <button class="floating-button" @click="$emit('toggle')">☰</button>
</template>

<style>
.floating-button {
  position: fixed;
  bottom: 20px;
  right: 20px;
  padding: 10px 15px;
  font-size: 24px;
  background-color: #333;
  color: white;
  border: none;
  border-radius: 50%;
  cursor: pointer;
  z-index: 9999;
}
</style>
