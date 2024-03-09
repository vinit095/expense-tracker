<script setup>
import Item from '@/components/Transactions/Item.vue'

defineProps({
  transactions: Object
})
let emit = defineEmits(['transactionDelete'])
let transactionDelete = (id) => {
  emit('transactionDelete', id)
}
</script>

<template>
  <h3>History</h3>

  <ul id="list" class="list">
      <Item v-for="(transaction, i) in transactions" :key="i" :transaction="transaction" @transactionDelete="transactionDelete" />
  </ul>

</template>