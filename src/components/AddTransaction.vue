<template>
    <form @submit.prevent="handleSubmit" class="md:flex mb-4 items-center gap-3">
      <input 
        v-model="title" 
        type="text" 
        placeholder="Title" 
        required 
        class="border p-2 text-white rounded w-full mb-2" 
      />
      
      <input 
        v-model.number="amount" 
        type="number" 
        placeholder="Amount" 
        required 
        class="border text-white p-2 rounded w-full mb-2" 
      />
      
      <select v-model="type" required class="border p-2 rounded w-full mb-2 text-amber-100">
        <option value="Income" class="bg-black">Income</option>
        <option value="Expense" class="bg-black">Expense</option>
      </select>
      
      <button type="submit" class="bg-blue-400 mb-2 text-white px-4 py-2 rounded w-full">Add</button>
    </form>
  </template>
  
  <script setup>
  import { ref, defineEmits } from 'vue';
  
  const emit = defineEmits(['add-transaction']);
  
  const title = ref('');
  const amount = ref(null);
  const type = ref('Income');
  
  const handleSubmit = () => {
    if (!title.value || amount.value <= 0) {
      alert('Please enter valid details.');
      return;
    }
    emit('add-transaction', { title: title.value, amount: amount.value, type: type.value });
    title.value = '';
    amount.value = null;
    type.value = 'Income';
  };
  </script>
    