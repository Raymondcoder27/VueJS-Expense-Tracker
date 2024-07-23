<template>
  <div>
    <h3>Add new Transaction</h3>
    <form @submit.prevent="onSubmit"  id="form">
      <div class="form-control">
        <label for="text">Text</label>
        <input
          type="text"
          id="text"
          placeholder="Enter text.."
          v-model="text"
        />
      </div>
      <div class="form-control">
        <label for="amount"
          >Amount <br />
          (negative - expense, positive - income)</label
        >
        <input
          type="text"
          id="amount"
          placeholder="Enter amount..."
          v-model="amount"
        />
      </div>
      <button class="btn">Add transaction</button>
    </form>
  </div>
</template>

<script setup>
import {ref} from 'vue'

  const text = ref('')
  const amount = ref('')

  const emit = defineEmits(['transactionSubmitted'])


  const onSubmit = () => {
  const transactionData = {
    text: text.value,
    amount: parseFloat(amount.value),
  }

  emit('transactionSubmitted', transactionData)

  text.value = '';
  amount.value = '';
    // console.log(text.value, amount.value)
  }
</script>
