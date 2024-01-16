<script setup>
import { ref, computed, onMounted } from 'vue';

import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import Total from './components/Total.vue';
import History from './components/History.vue';
import AddUserInput from './components/AddUserInput.vue';

// Transaction data
const transactionsData = ref(
  []
);

// Check if local storage has data
onMounted(() => {
  const savedData = JSON.parse(localStorage.getItem("transactionsData"));

  if (savedData) {
    transactionsData.value = savedData;
  }
});

// Get total
const total = computed(() => {
  return transactionsData.value.reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0).toFixed(2);
});

// Get income
const income = computed(() => {
  return transactionsData.value
  .filter((transaction) => transaction.amount > 0 )
  .reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0).toFixed(2);
});

// Get expense
const expense = computed(() => {
  return transactionsData.value
  .filter((transaction) => transaction.amount < 0 )
  .reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0).toFixed(2);
});


// Adding user input to transactionsData array
const handleUserInput = (userData) => {
  transactionsData.value.push({
    id: transactionsData.value.length,
    text: userData.text,
    amount: userData.sign === "expense" ? userData.amount * -1 : userData.amount,
  })

  saveLocal();
  //console.log(userData);
}

// Removing data from transactionsData array
const handleRemoveData = (id) => {
  transactionsData.value = transactionsData.value.filter((transaction) => transaction.id !== id );
  //console.log(id);
  saveLocal();
}

// Save data to local storage
const saveLocal = () => {
  localStorage.setItem("transactionsData", JSON.stringify(transactionsData.value));
}
</script>

<template>
  <Header />
  <hr />
  
  <div class="container">

    <Balance :total="+total"/>
    <hr />

    <Total :income="+income" :expense="+expense"/>
    <hr />

    <History :transactions="transactionsData" @removeHistoryData="handleRemoveData"/>
    <hr />

    <AddUserInput @receivedUserInput="handleUserInput"/>
  </div>

</template>

<style scoped>

</style>
