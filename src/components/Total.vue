<script setup>
    // Define props - receive income, expense from App
    const props = defineProps({
        income: {
            type: Number,
            required: true,
        },
        expense: {
            type: Number,
            required: true,
        }
    });
    
</script>

<template>
    <div class="row">
        <div class="col">
            <strong>Income: $ <span style="color: green;">{{ income }}</span></strong>
        </div>

        <div class="col">
            <strong>Expense: $ <span style="color: red;">{{ expense }}</span></strong>
        </div>
    </div>
</template>

<style scoped>
</style>