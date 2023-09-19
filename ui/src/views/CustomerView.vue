<template>
    <div class="d-flex justify-content-between align-items-center">
        <div>
            <h1>View Customer</h1>
        </div>
    </div>
    <div class="d-flex justify-content-end">
        <button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#exampleModal" @click="add()">
            Add Customer
        </button>
    </div>
    <table class="table table-striped table-hover">
        <thead>
            <tr>
                <th>Customer ID</th>
                <th>Customer Name</th>
                <th>Phone</th>
                <th>Email</th>
                <th>Address</th>
                <th>Account No.</th>
                <th>Action</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="cust in customers" :key="cust.id">
                <td>{{ cust.CustomerId }}</td>
                <td>{{ cust.CustomerName }}</td>
                <td>{{ cust.CustomerPhone }}</td>
                <td>{{ cust.CustomerEmail }}</td>
                <td>{{ cust.CustomerAddress }}</td>
                <td>{{ cust.AccountNumber }}</td>
                <td>
                    <button type="button" class="btn btn-primary m-2 fload-end" data-bs-toggle="modal"
                        data-bs-target="#exampleModal" @click="edit(cust)">
                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor"
                            class="bi bi-pencil-square" viewBox="0 0 16 16">
                            <path
                                d="M15.502 1.94a.5.5 0 0 1 0 .706L14.459 3.69l-2-2L13.502.646a.5.5 0 0 1 .707 0l1.293 1.293zm-1.75 2.456-2-2L4.939 9.21a.5.5 0 0 0-.121.196l-.805 2.414a.25.25 0 0 0 .316.316l2.414-.805a.5.5 0 0 0 .196-.12l6.813-6.814z" />
                            <path fill-rule="evenodd"
                                d="M1 13.5A1.5 1.5 0 0 0 2.5 15h11a1.5 1.5 0 0 0 1.5-1.5v-6a.5.5 0 0 0-1 0v6a.5.5 0 0 1-.5.5h-11a.5.5 0 0 1-.5-.5v-11a.5.5 0 0 1 .5-.5H9a.5.5 0 0 0 0-1H2.5A1.5 1.5 0 0 0 1 2.5v11z" />
                        </svg>
                    </button>
                    <button type="button" class="btn btn-danger mr-1" @click="remove(cust.CustomerId)">
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
                        <div class="col-12">
                            <div class="form-floating">
                                <input type="text" class="form-control" id="floatingInputGrid" v-model="CustomerName"
                                    placeholder="name">
                                <label for="floatingInputGrid">Customer Name</label>
                            </div>
                        </div>
                        <div class="col-md-6">
                            <div class="form-floating">
                                <input type="text" class="form-control" id="floatingInputGrid" v-model="CustomerPhone"
                                    placeholder="">
                                <label for="floatingInputGrid">Phone</label>
                            </div>
                        </div>
                        <div class="col-md-6">
                            <div class="form-floating">
                                <input type="email" class="form-control" id="floatingInputGrid" v-model="CustomerEmail"
                                    placeholder="name@example.com">
                                <label for="floatingInputGrid">Email Address</label>
                            </div>
                        </div>
                        <div class="col-md-8">
                            <div class="form-floating">
                                <input type="text" class="form-control" id="floatingInputGrid" v-model="CustomerAddress"
                                    placeholder="">
                                <label for="floatingInputGrid">Address</label>
                            </div>
                        </div>
                        <div class="col-md-4">
                            <div class="form-floating">
                                <select class="form-select" id="floatingSelectGrid" v-model="AccountNumber"
                                    aria-label="Floating label select example">
                                    <option v-for="acc in accounts" :key="acc.id">{{ acc.AccountNumber }}</option>
                                </select>
                                <label for="floatingSelectGrid">Account No.</label>
                            </div>
                        </div>
                        <div class="col-12">
                            <button type="button" @click="create()" v-if="CustomerId == 0"
                                class="btn btn-primary">Create</button>
                            <button type="button" @click="update()" v-if="CustomerId != 0"
                                class="btn btn-primary">Update</button>
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
            customers: [],
            accounts: [],
            modalTitle: "",
            CustomerId: 0,
            CustomerName: "",
            CustomerPhone: "",
            CustomerEmail: "",
            CustomerAddress: "",
            AccountNumber: "",
        };
    },
    methods: {
        refreshData() {
            axios.get(variable.API_URL + "customer")
                .then((response) => {
                    this.customers = response.data;
                });

            axios.get(variable.API_URL + "account")
                .then((response) => {
                    this.accounts = response.data;
                });
        },
        add() {
            this.modalTitle = "Add Customer";
            this.CustomerId = 0;
            this.CustomerName = "";
            this.CustomerPhone = "";
            this.CustomerEmail = "";
            this.CustomerAddress = "";
            this.AccountNumber = "";
        },
        edit(cust) {
            this.modalTitle = "Edit Customer";
            this.CustomerId = cust.CustomerId;
            this.CustomerName = cust.CustomerName;
            this.CustomerPhone = cust.CustomerPhone;
            this.CustomerEmail = cust.CustomerEmail;
            this.CustomerAddress = cust.CustomerAddress;
            this.AccountNumber = cust.AccountNumber;
        },
        create() {
            axios.post(variable.API_URL + "customer", {
                CustomerName: this.CustomerName,
                CustomerPhone: this.CustomerPhone,
                CustomerEmail: this.CustomerEmail,
                CustomerAddress: this.CustomerAddress,
                AccountNumber: this.AccountNumber,
            })
                .then((response) => {
                    this.refreshData();
                    alert(response.data);
                });
        },
        update() {
            axios.post(variable.API_URL + "customer/edit/" + this.CustomerId, {
                CustomerId: this.CustomerId,
                CustomerName: this.CustomerName,
                CustomerPhone: this.CustomerPhone,
                CustomerEmail: this.CustomerEmail,
                CustomerAddress: this.CustomerAddress,
                AccountNumber: this.AccountNumber,
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
            axios.post(variable.API_URL + "customer/delete/" + id)
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