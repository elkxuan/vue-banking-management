<template>
    <div class="d-flex justify-content-between align-items-center">
        <div>
            <h1>View Account</h1>
        </div>
    </div>
    <div class="d-flex justify-content-end">
        <button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#exampleModal" @click="add()">
            Add Account
        </button>
    </div>
    <table class="table table-striped table-hover">
        <thead>
            <tr>
                <th>Account Number</th>
                <th>Account Type</th>
                <th>Customer ID</th>
                <th>Balance</th>
                <th>Status</th>
                <th>Action</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="acc in accounts" :key="acc.id">
                <td>{{ acc.AccountNumber }}</td>
                <td>{{ acc.AccountType }}</td>
                <td>{{ acc.CustomerId }}</td>
                <td>RM {{ acc.Balance }}</td>
                <td>{{ acc.Status }}</td>
                <td>
                    <button type="button" class="btn btn-primary me-1" data-bs-toggle="modal" data-bs-target="#exampleModal"
                        @click="edit(acc)">
                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor"
                            class="bi bi-pencil-square" viewBox="0 0 16 16">
                            <path
                                d="M15.502 1.94a.5.5 0 0 1 0 .706L14.459 3.69l-2-2L13.502.646a.5.5 0 0 1 .707 0l1.293 1.293zm-1.75 2.456-2-2L4.939 9.21a.5.5 0 0 0-.121.196l-.805 2.414a.25.25 0 0 0 .316.316l2.414-.805a.5.5 0 0 0 .196-.12l6.813-6.814z" />
                            <path fill-rule="evenodd"
                                d="M1 13.5A1.5 1.5 0 0 0 2.5 15h11a1.5 1.5 0 0 0 1.5-1.5v-6a.5.5 0 0 0-1 0v6a.5.5 0 0 1-.5.5h-11a.5.5 0 0 1-.5-.5v-11a.5.5 0 0 1 .5-.5H9a.5.5 0 0 0 0-1H2.5A1.5 1.5 0 0 0 1 2.5v11z" />
                        </svg>
                    </button>
                    <button type="button" class="btn btn-danger me-1" @click="remove(acc.AccountId)">
                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor"
                            class="bi bi-trash" viewBox="0 0 16 16">
                            <path
                                d="M5.5 5.5A.5.5 0 0 1 6 6v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5Zm2.5 0a.5.5 0 0 1 .5.5v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5Zm3 .5a.5.5 0 0 0-1 0v6a.5.5 0 0 0 1 0V6Z" />
                            <path
                                d="M14.5 3a1 1 0 0 1-1 1H13v9a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V4h-.5a1 1 0 0 1-1-1V2a1 1 0 0 1 1-1H6a1 1 0 0 1 1-1h2a1 1 0 0 1 1 1h3.5a1 1 0 0 1 1 1v1ZM4.118 4 4 4.059V13a1 1 0 0 0 1 1h6a1 1 0 0 0 1-1V4.059L11.882 4H4.118ZM2.5 3h11V2h-11v1Z" />
                        </svg>
                    </button>
                </td>
            </tr>
        </tbody>
    </table>

    <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog modal-lg modal-dialog-centered">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title" id="exampleModalLabel">{{ modalTitle }}</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body">
                    <div class="row g-3">
                        <div class="col-md-8">
                            <div class="form-floating">
                                <input type="text" class="form-control" id="floatingInputGrid" v-model="AccountNumber"
                                    placeholder="account number">
                                <label for="floatingInputGrid">Account Number</label>
                            </div>
                        </div>
                        <div class="col-md-4">
                            <div class="form-floating">
                                <select class="form-select" id="floatingSelectGrid" v-model="AccountType"
                                    aria-label="Floating label select example">
                                    <option>Savings Account</option>
                                    <option>Current Account</option>
                                    <option>Fixed Deposit Account</option>
                                </select>
                                <label for="floatingSelectGrid">Account Type</label>
                            </div>
                        </div>
                        <div class="col-md-6">
                            <div class="form-floating">
                                <input type="text" class="form-control" id="floatingInputGrid" v-model="CustomerId"
                                    placeholder="id">
                                <label for="floatingInputGrid">Customer ID</label>
                            </div>
                        </div>
                        <div class="col-md-6">
                            <div class="form-floating">
                                <input type="text" class="form-control" id="floatingInputGrid" v-model="Balance"
                                    placeholder="RM">
                                <label for="floatingInputGrid">Balance</label>
                            </div>
                        </div>
                        <div class="col-md-6">
                            <div class="form-floating">
                                <select class="form-select" id="floatingSelectGrid" v-model="Status"
                                    aria-label="Floating label select example">
                                    <option>Active</option>
                                    <option>Inactive</option>
                                </select>
                                <label for="floatingSelectGrid">Status</label>
                            </div>
                        </div>
                        <div class="col-12">
                            <button type="button" @click="create()" v-if="AccountId == 0"
                                class="btn btn-primary" data-bs-dismiss="modal">Create</button>
                            <button type="button" @click="update()" v-if="AccountId != 0"
                                class="btn btn-primary" data-bs-dismiss="modal">Update</button>
                        </div>
                    </div>

                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
import variable from '../variable';

export default {
    data() {
        return {
            accounts: [],
            customers: [],
            modalTitle: "",
            AccountId: 0,
            AccountNumber: "",
            AccountType: "",
            CustomerId: "",
            Balance: "",
            Status: "",
            Amount: 0
        };
    },
    methods: {
        refreshData() {
            axios.get(variable.API_URL + "account")
                .then((response) => {
                    this.accounts = response.data;
                });

            axios.get(variable.API_URL + "customer")
                .then((response) => {
                    this.customers = response.data;
                });
        },
        add() {
            this.modalTitle = "Add Account";
            this.AccountId = 0;
            this.AccountNumber = "";
            this.AccountType = "";
            this.CustomerId = "";
            this.Balance = "";
            this.Status = "";
        },
        edit(acc) {
            this.modalTitle = "Edit Account";
            this.AccountId = acc.AccountId;
            this.AccountNumber = acc.AccountNumber;
            this.AccountType = acc.AccountType;
            this.CustomerId = acc.CustomerId;
            this.Balance = acc.Balance;
            this.Status = acc.Status;
        },
        create() {
            axios.post(variable.API_URL + "account", {
                AccountNumber: this.AccountNumber,
                AccountType: this.AccountType,
                CustomerId: this.CustomerId,
                Balance: this.Balance,
                Status: this.Status
            })
                .then((response) => {
                    this.refreshData();
                    alert(response.data);
                });
        },
        update() {
            axios.post(variable.API_URL + "account/edit/" + this.AccountId, {
                AccountId: this.AccountId,
                AccountNumber: this.AccountNumber,
                AccountType: this.AccountType,
                CustomerId: this.CustomerId,
                Balance: this.Balance,
                Status: this.Status
            })
                .then((response) => {
                    this.refreshData();
                    alert(response.data);
                });
        },
        remove(id) {
            if (!confirm("Are you sure to remove?")) {
                return;
            }
            axios.post(variable.API_URL + "account/delete/" + id)
                .then((response) => {
                    this.refreshData();
                    alert(response.data);
                });
        },
    },
    mounted: function () {
        this.refreshData();
    }
}
</script>