<script setup>

// Receiving props (transactionsData array from App)
const props = defineProps({
    transactions: {
        type: Array,
        required: true,
    }
});

// Define emiting event
const emits = defineEmits(["removeHistoryData"]);

// Emiting/ Sending event to App (remove button click)
const removeData = (id) => {
    emits("removeHistoryData", id);
};

</script>

<template>
    <div>
        <h3 class="">Transaction History:</h3>
        <hr />
        <ul class="list-group">
            <li v-for="transaction in transactions" :key="transaction.id" class="list-group-item d-flex justify-content-between align-items-start">
                <div class="ms-2 me-auto">
                    {{ transaction.text }}
                </div>
                <div class="me-3">
                    $ {{ transaction.amount }}
                </div>
                <div>
                    <button @click="removeData(transaction.id)" class="btn-close" type="button"></button>
                </div>
            </li>
        </ul>
    </div>
</template>

<style scoped>
</style>