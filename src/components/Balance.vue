<script setup>
    // Define props - receive total from App
    const props = defineProps({
        total: {
            type: Number,
            required: true,
        }
    });
    
</script>

<template>
    <div class="">
        <h2>Balance: $ {{ total }}</h2>
    </div>
</template>

<style scoped>
</style>