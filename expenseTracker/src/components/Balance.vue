<template>
    <div>
    <h4>YOUR BALANCE</h4>
    <h1 id="balance">UGX. {{ total }}</h1>
    </div>
</template>

<script setup>
    import { defineProps } from 'vue';
    const props = defineProps({
        total: {
            type: Number,
            required: true,
        }
    });
</script>

