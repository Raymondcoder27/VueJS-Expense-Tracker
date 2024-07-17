<template>
  <div>
  <Header />
  <div class="container">
    <Balance :total="+total" />
    <IncomeExpenses :income="+income" :expenses="+expenses" />
    <TransactionList :transactions="transactions" 
    @transactionDeleted="handleTransactionDeleted" />
    <AddTransaction @transaction-submitted="handleTransactionSubmitted" />
  </div>
  </div>
</template>

<script setup>
  import Header from "./components/Header.vue"
  import Balance from "./components/Balance.vue"
  import IncomeExpenses from "./components/IncomeExpenses.vue"
  import TransactionList from "./components/TransactionalList.vue"
  import AddTransaction from "./components/AddTransaction.vue"

  import { computed, onMounted, ref } from 'vue'

  // const transactions = ref([
  //       {id: 1, text: 'Flower', amount: -19.99},
  //       {id: 2, text: 'Salary', amount: 219.99},
  //       {id: 3, text: 'Book', amount: -10},
  //       {id: 4, text: 'Camera', amount: 150},
  //   ]);

  const transactions = ref([]);

  onMounted(()=>{
    const savedTransactions = JSON.parse(localStorage.getItem('transactions'));
    if (savedTransactions) {
      transactions.value = savedTransactions;
    }
  })

  //get total
    const total = computed(()=>{
      return transactions.value.reduce((acc, transaction) =>{
        return acc + transaction.amount
      }, 0)
    })

    //get income
    const income = computed(()=> {
      return transactions.value
      .filter((transaction)=> transaction.amount > 0)
      .reduce((acc, transaction)=>{
        return acc + transaction.amount
      },0)
      .toFixed(2)
    })

    //get expenses
    const expenses = computed(()=> {
      return transactions.value
      .filter((transaction) => transaction.amount < 0)
      .reduce((acc, transaction)=>{
        return acc + transaction.amount
      }, 0)
      .toFixed(2)
    })

    // const addTransaction = () =>{
    //   transactions.value.reduce(
    //   )
    // }

    //add transaction
    const handleTransactionSubmitted = (transactionData) =>{
      transactions.value.push({
        id: generateUniqueId(), 
        text: transactionData.text,
        amount: transactionData.amount
      });

      console.log(generateUniqueId())
      saveTransactionsToLocalStorage()

    alert("hello")
    alert("hello")
    alert("hello")

    };
    // alert("hello")


    //generate unique id
    const generateUniqueId = () => {
      return Math.floor(Math.random() * 100000);
    }

    const handleTransactionDeleted = (id) => {
      transactions.value = transactions.value.filter((transaction)=>
      transaction.id != id );

      saveTransactionsToLocalStorage()
    }

    //save to localstorage
    const saveTransactionsToLocalStorage = () => {
      localStorage.setItem('transactions', JSON.stringify(transactions.value));
    }
</script>