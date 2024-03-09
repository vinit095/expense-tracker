<script setup>
import { useToast } from 'vue-toastification'
import { v4 as uuidv4 } from 'uuid'
import { ref } from 'vue'

let emit = defineEmits(['transactionAdd'])
let amount = ref('')
let text = ref('')
let toast = useToast()
let submitForm = () => {
  if(!amount.value || !text.value){
    toast.error('Both fields must be filled')
    return
  }
  emit('transactionAdd', {
    id: uuidv4(),
    text: text.value,
    amount: amount.value
  })
  text.value = amount.value = "";
  toast.success('Event added successfully')
}
</script>

<template>
  <h3>Add new transaction</h3>
  <form id="form" @submit.prevent="submitForm">
    <div class="form-control">
      <label for="text">Text</label>
      <input type="text" id="text" placeholder="Enter text..." v-model="text" />
    </div>
    <div class="form-control">
      <label for="amount"
      >Amount <br />
        (negative - expense, positive - income)</label
      >
      <input type="number" id="amount" placeholder="Enter amount..." v-model="amount" />
    </div>
    <button class="btn">Add transaction</button>
  </form>
</template>