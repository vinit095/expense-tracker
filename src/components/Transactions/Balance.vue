<script setup>
defineProps({
  balance: Number
})
</script>

<template>
  <h4>Your Balance</h4>
  <h1 id="balance">${{ balance }}</h1>
</template>