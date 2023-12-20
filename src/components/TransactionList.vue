<script setup>
   import { defineProps } from 'vue';

   const emit = defineEmits(['transactionDeleted']);

   const deleteTransaction = (id) => {
    emit('transactionDeleted', id);
   }

   const props = defineProps({
    transactions: {
        type: Array,
        required: true,
    },
   });
</script>

<template>
    <h3>History</h3>
    <ul id="list" class="list">
        <li v-for="transaction in transactions" :key="transaction.id" :class="transaction.amount < 0 ? 'minus' : 'plus'">
            {{ transaction.text }} <span>${{ transaction.amount }}</span><button class="delete-btn">x</button>
        </li>
        <li class="minus">
            Cash <span>-$500</span><button class="delete-btn" @click="deleteTransaction(transaction.id)">x</button>
        </li>
        <li class="plus">
            Salary <span>+1000</span><button class="delete-btn" @click="deleteTransaction(transaction.id)">x</button>
        </li>
    </ul>

    
</template>