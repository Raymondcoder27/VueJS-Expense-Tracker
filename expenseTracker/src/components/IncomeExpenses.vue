<template>
    <div class="inc-exp-container">
        <div>
            <h4>Income</h4>
            <p id="money-plus" class="money plus">
                UGX. {{income}}
            </p>
        </div>
        <div>
            <h4>Expenses</h4>
            <p id="money-minus" class="money minus">
                UGX. {{expenses}}
            </p>
        </div>
    </div>
</template>


<script setup>
    const props = defineProps({
        income:{
        type: Number,
        required: true,
        },
        expenses:{
            type: Number,
            required: true
        }
    })
</script>
