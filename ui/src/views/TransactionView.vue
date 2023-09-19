<template>
    <div class="d-flex justify-content-between align-items-center">
        <div>
            <h1>View Transaction</h1>
        </div>
    </div>
    <table class="table table-striped table-hover">
        <thead>
            <tr>
                <th>Transaction ID</th>
                <th>Account No.</th>
                <th>Date</th>
                <th>Transaction Type</th>
                <th>Status</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="trx in transactions" :key="trx.id">
                <td>{{ trx.TransactionId }}</td>
                <td>{{ trx.AccountNumber }}</td>
                <td>{{ trx.TransactionDate }}</td>
                <td>{{ trx.TransactionType }}</td>
                <td>{{ trx.Status }}</td>
            </tr>
        </tbody>
    </table>
</template>

<script>
import axios from 'axios';
import variable from '../variable';

export default {
    data() {
        return {
            transactions: [],
            TransactionId: 0,
            AccountNumber: "",
            TransactionDate: "",
            TransactionType: "",
            Status: ""
        };
    },
    methods: {
        refreshData() {
            axios.get(variable.API_URL + "transaction")
                .then((response) => {
                    this.transactions = response.data;
                });
        },
    },
    mounted: function () {
        this.refreshData();
    }
}
</script>