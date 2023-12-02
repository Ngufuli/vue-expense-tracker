<script setup>
  import Header from './components/Header.vue';
  import Balance from './components/Balance.vue';
  import IncomeExpense from './components/IncomeExpense.vue';
  import TransactionList from './components/TransactionList.vue';
  import AddTransactionVue from './components/AddTransaction.vue';
  import {ref} from 'vue';

  const transactions = [
        {id: 1, text: 'Flower', amount: -19.00},
        {id: 2, text: 'Salary', amount: 299.97},
        {id: 3, text: 'Book', amount: -10},
        {id: 4, text: 'Camera', amount: 150}
    ]
</script>

<template>
  <Header />
  <div class="container">
    <Balance />
    <IncomeExpense />
    <TransactionList />
    <AddTransactionVue />
  </div>
</template>