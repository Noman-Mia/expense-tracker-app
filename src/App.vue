<template>
  <div class="container mx-auto p-4 pt-20">
    <h1 class="text-2xl font-bold text-center mb-4 text-blue-400 pb-5">
      Expense Tracker
    </h1>
    <AddTransaction @add-transaction="addTransaction" />
    <TransactionList 
      :transactions="transactions" 
      @delete-transaction="deleteTransaction"
    />
  </div>
</template>

<script setup>
import { ref, onMounted, watch } from 'vue';
import AddTransaction from './components/AddTransaction.vue';
import TransactionList from './components/TransactionList.vue';

const transactions = ref([]);

onMounted(() => {
  const storedTransactions = localStorage.getItem('transactions');
  if (storedTransactions) {
    transactions.value = JSON.parse(storedTransactions);
  }
});

const saveTransactions = () => {
  localStorage.setItem('transactions', JSON.stringify(transactions.value));
};


watch(transactions, saveTransactions, { deep: true });

const addTransaction = (transaction) => {
  if (transaction.amount <= 0) {
    alert("Amount must be greater than 0");
    return;
  }
  transactions.value.push(transaction);
};

const deleteTransaction = (index) => {
  transactions.value.splice(index, 1);
};
</script>

