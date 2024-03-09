<script setup>
import { useToast } from 'vue-toastification'
defineProps({
  transaction: Object
})
let emit = defineEmits(['transactionDelete'])
let toast = useToast()
let transactionDelete = (id) => {
  emit('transactionDelete', id)
  toast.success('Transaction deleted!')
}
</script>

<template>
  <li :class="{
    'minus' : transaction.amount < 0,
    'plus'  : transaction.amount > 0
  }">
        {{ transaction.text }}
    <span>${{ transaction.amount }}</span>
    <button class="delete-btn"
            @click="transactionDelete(transaction.id)"
    >x</button>
      </li>
</template>