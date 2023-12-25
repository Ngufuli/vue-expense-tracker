<script setup>
  import Header from './components/Header.vue';
  import Balance from './components/Balance.vue';
  import IncomeExpense from './components/IncomeExpense.vue';
  import TransactionList from './components/TransactionList.vue';
  import AddTransaction from './components/AddTransaction.vue';
  import {computed, ref} from 'vue';
  import { useToast } from 'vue-toastification';
  import {ref, computed, onMounted} from 'vue';

  const toast = useToast();
  const transactions = ref([]);

  onMounted(() => {
    const savedTransactions = JSON.parse(localStorage.getItem('transactions'));

    if(savedTransactions){
      transactions.value = savedTransactions;
    }
  })
  // const transactions = ref([
  //       {id: 1, text: 'Flower', amount: -19.00},
  //       {id: 2, text: 'Salary', amount: 299.97},
  //       {id: 3, text: 'Book', amount: -10},
  //       {id: 4, text: 'Camera', amount: 150}
  //   ])

  const saveTransactionsToLocalStorage = () => {
    localStorage.setItem('transactions', JSON.stringify(transactions.value));
  };

    // get total
    const total = computed(() => {
    return transactions.value.reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0);
  });

    // get income
    const income = computed(() => {
      return transactions.value
        .filter((transaction) => transaction.amount > 0)
        .reduce((acc, transaction) => acc + transaction.amount, 0)
        .toFixed(2);
    });

    // get expenses
    const expenses = computed(() => {
      return transactions.value
        .filter((transaction) => transaction.amount < 0)
        .reduce((acc, transaction) => acc + transaction.amount, 0)
        .toFixed(2)
    })

    const generateUniqueId = () => {
      return Math.floor(Math.random() * 1000000)
    }

    const handleTransactionSubmitted = (transactionData) => {
      // console.log(transactionData);
      transactions.value.push({
        id: generateUniqueId(),
        text: transactionData.text,
        amount:transactionData.amount
      });

      saveTransactionsToLocalStorage();

      toast.success('Transaction added')
    }

   

    const handleTransactionDeleted = (id) => {
      transactions.value = transactions.value.filter(
        (transaction) => transaction.id != id
      );
      saveTransactionsToLocalStorage();
      
      toast.success('Transaction deleted');
    }
</script>

<template>
  <Header />
  <div class="container">
    <Balance :total="total" />
    <IncomeExpense :income="+income" :expenses="+expenses" />
    <TransactionList :transactions="transactions" @transactionDeleted="handleTransactionDeleted"/>
    <AddTransaction @transactionSubmitted="handleTransactionSubmitted"/>
  </div>
</template>