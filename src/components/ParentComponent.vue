<script setup>
defineProps({
  cart: Array,
});
</script>
<template>
  <div>
    <div class="icecream" id="icecream">
      <p class="cone"></p>
      <div
        class="scoop"
        v-for="(cartItem, index) in cart"
        :key="index"
        :class="cartItem.name.toLowerCase()"
      ></div>
      <div class="cherry" v-if="cart.length > 0"></div>
      <div class="question" v-else></div>
    </div>
  </div>
</template>
