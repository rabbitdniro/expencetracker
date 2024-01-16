<script setup>
import {ref} from 'vue';

const text = ref("");
const amount = ref("");
const sign = ref("");

// Define emits
const emits = defineEmits(["receivedUserInput"]);

// Get user input
const addIncomeExpense = () => {
    if (!text.value || !amount.value || !sign.value) {
        alert("Input field cannot be empty!");

    } else {
        const userData = {
            text: text.value,
            amount: parseFloat(amount.value),
            sign: sign.value,
        }
        
        // Emits user input to App
        emits("receivedUserInput", userData);
    
        text.value = "";
        amount.value = "";
        sign.value = "";
    }
};

// Modal popup
function showPopup() {
    modal.showModal();
}

function closePopup() {
    modal.close();
}
</script>

<template>
    <div>
        <button @click="showPopup()" type="button" class="btn btn-primary">Add Transaction</button>

        <dialog id="modal" style="border: none;">
            <div class="card">
                <div class="card-body">
                    <form @submit.prevent="addIncomeExpense()" action="">
                        <div class="row mb-3 align-items-center">
                            <div class="input-group">
                                <div class="input-group-text"><strong>Details</strong></div>
                                <input v-model="text" type="text" name="" id="" placeholder="Write something" class="form-control">
                            </div>
                        </div>

                        <div class="row mb-3 align-items-center">
                            <div class="input-group">
                                <div class="input-group-text"><strong>Amount</strong></div>
                                <input v-model="amount" type="text" name="" id="" placeholder="150.50" class="form-control">
                            </div>
                        </div>

                        <div class="row mb-3 align-items-center">
                            <div class="input-group">
                                <div class="input-group-text"><strong>In/Out?</strong></div>
                                <select v-model="sign" id="" class="form-select">
                                    <option value="" selected>Please select</option>
                                    <option value="income">Income</option>
                                    <option value="expense">Expense</option>
                                </select>
                            </div>
                        </div>

                        <div class="row align-items-center">
                            <div class="col">
                                <button @click="addIncomeExpense(); closePopup()" type="button" name="" id="" class="btn btn-primary">Submit</button>
                            </div>
                            <div class="col">
                                <button @click="closePopup()" type="button" name="" id="" class="btn btn-primary">Close</button>
                            </div>
                        </div>
                    </form>
                </div>
            </div>
        </dialog>
    </div>
</template>

<style scoped>
</style>