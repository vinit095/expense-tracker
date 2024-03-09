<script setup>

import Transactions from '@/components/Transactions/Transactions.vue'
import Balance from '@/components/Transactions/Balance.vue'
import IncomeExpense from '@/components/Transactions/IncomeExpense.vue'
import Add from '@/components/Transactions/Add.vue'
import { computed, onMounted, ref } from 'vue'

let transactions = ref([
  { id:1, text: 'Salary', amount: 20000},
  { id:2, text: 'Milk', amount: -360},
  { id:3, text: 'Rent', amount: -3000},
  { id:4, text: 'News paper', amount: -500}
])

onMounted(() => {
  const savedTransactions = JSON.parse(localStorage.getItem('transactions'))
  if(savedTransactions) transactions.value = savedTransactions
})

// Get Total balance
const balance = computed(() => {
  return transactions.value.reduce((acc, b) => {
    return acc + b.amount
  }, 0)
})

// Get total expenses
let expenses =  computed(() => {
  return transactions.value.filter(a => a.amount < 0).
          reduce((acc, b) => {
            return acc + b.amount
          }, 0)
})

// Get total income
let income = computed(() => {
  return transactions.value.filter(a => a.amount > 0).
  reduce((acc, b) => {
    return acc + b.amount
  }, 0)
})

let transactionSave = () => {
  localStorage.setItem('transactions', JSON.stringify(transactions.value))
}

// Add transaction function
let transactionAdd = (transactionData) => {
  transactions.value.push(transactionData)
  transactionSave()
}
let transactionDelete = (id) => {
  transactions.value =  transactions.value.filter(transaction => transaction.id !== id)
  transactionSave()
}
</script>

<template>
  <h2>Expense Tracker</h2>

  <div class="container">
    <Balance :balance="balance" />

    <IncomeExpense :expenses="expenses" :income="income" />

    <Transactions :transactions="transactions" @transactionDelete="transactionDelete" />

    <Add @transactionAdd="transactionAdd" />
  </div>
</template>