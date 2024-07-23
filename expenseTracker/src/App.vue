<template>
  <div>
    <Header />
    <Balance :total="+total" />
    <IncomeExpenses :income="+income" :expenses="+expenses" />
    <TransactionalList :transactions="transactions" 
    @transactionDeleted="handleTransactionDeleted"/>
    <AddTransaction 
    @transactionSubmitted="handleSubmission"
   />
  </div>
</template>

<script  setup>
  import Header from './components/Header.vue';
  import Balance from './components/Balance.vue';
  import IncomeExpenses from './components/IncomeExpenses.vue';
  import TransactionalList from './components/TransactionalList.vue';
  import AddTransaction from './components/AddTransaction.vue';

  import {ref, computed, onMounted} from 'vue'
  // const total = ref(0)
  const transactions = ref([])

  onMounted(()=>{
    const savedTransactions = JSON.parse(localStorage.getItem
    ('transactions'))

    if (savedTransactions) {
      transactions.value = savedTransactions
    }
  })


  const total = computed(()=>{
    return transactions.value.reduce((acc, transaction) => {
      return acc + transaction.amount
    }, 0)
  })

  //get income
  const income = computed(()=> {
    return transactions.value
    .filter((transaction)=>transaction.amount > 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount
    }, 0).toFixed(2)
  })

  //get expenses
  const expenses = computed(()=>{
    return transactions.value
    .filter((transaction)=> transaction.amount < 0)
    .reduce((acc, transaction)=> {
      return  acc + transaction.amount;
    },0).toFixed(2)
  })

  const handleSubmission = (transactionData) => {
    // console.log(transactionData.text)
    transactions.value.push({
      id: generatedId(),
      text: transactionData.text,
      amount: transactionData.amount
    })

    saveTransactionsToLocalStorage()

    // transactions = localStorage.setItem(json.stringify())
  }

  const generatedId = () => {
    return Math.floor(Math.random() * 10000)
  }

  const handleTransactionDeleted = (id) => {
    // console.log(id)
    transactions.value = transactions.value.filter(
      (transaction)=> transaction.id !== id 
      )
    // transactions.id != id
    saveTransactionsToLocalStorage()
  }
  
  //save to localstorage
  const saveTransactionsToLocalStorage = () => {
    localStorage.setItem('transactions', JSON.stringify(transactions.value))
  }

</script>

