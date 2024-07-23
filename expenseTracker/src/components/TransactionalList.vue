<template>
  <div>
  <h3>History</h3>
  <ul id="list" class="list">
    <li
    v-for="transaction in transactions"
    :key="transaction.id"
    :class="transaction.amount < 0 ? 'minus' : 'plus'">
    <button @click="deleteTransaction(transaction.id)" class="delete-btn">x</button>
    {{ transaction.text }} <span> {{ transaction.amount }}</span>
    </li>
    <!-- <li class="minus">
      Cash <span>$400</span>
      <button class="delete-btn">x</button>
    </li>
    <li class="plus">
        Paycheck <span>$200</span>
        <button class="delete-btn">x</button>
    </li> -->
  </ul>
</div>
</template>

<script setup>
  const props = defineProps({
    transactions: {
      type: Array,
      required: true
    }
  })

  const emit = defineEmits(['transactionDeleted'])

  const deleteTransaction = (id) =>{
    // console.log('deleted',id)
    emit('transactionDeleted', id);
  }
</script>

