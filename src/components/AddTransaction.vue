<script setup>
import { ref } from 'vue';
import { useToast } from 'vue-toastification';

const text = ref('');
const amount = ref('');

const emit = defineEmits(['transactionSubmitted']);

//Get toast interface
const toast = useToast();

const onSubmit = () => {
    if(!text.value || !amount.value){
        //Display a toast error message if either field is empty
        toast.error('Both fields must be filled.');
        return;
    }

    //Proceed with form submission login here...
    // console.log(('Form submitted:', text.value, amount.value));

    //Emit a custom event with the transaction data
    const transactionData = {
        text: text.value,
        amount: parseFloat(amount.value),
    }

    emit('transactionSubmitted', transactionData);
    //clear form fields
    text.value = '';
    amount.value = '';
}

</script>

<template>
    <h3>Add new transaction</h3>
    <form id="form" @submit.prevent="onSubmit">
        <div class="form-control" >
            <label for="text">Text</label>
            <input type="text" id="text" placeholder="Enter text..." v-model="text"/>
        </div>
        <div class="form-control">
            <label for="amount">Amount <br/>(negative - expense, positive - income)</label>
            <input type="text" id="amount" placeholder="Enter amount..." v-model="amount"/>
        </div>
        <button class="btn">Add transaction</button>
    </form>
</template>