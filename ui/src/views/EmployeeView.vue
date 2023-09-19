<template>
    <div class="d-flex justify-content-between align-items-center">
        <div>
            <h1>View Employee</h1>
        </div>
    </div>
    <div class="d-flex justify-content-end">
        <button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#exampleModal" @click="add()">
            Add Employee
        </button>
    </div>
    <table class="table table-striped table-hover">
        <thead>
            <tr>
                <th>Employee ID</th>
                <th>Employee Name</th>
                <th>Phone</th>
                <th>Email</th>
                <th>Department</th>
                <th>Action</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="emp in employees" :key="emp.id">
                <td>{{ emp.EmployeeId }}</td>
                <td>{{ emp.EmployeeName }}</td>
                <td>{{ emp.EmployeePhone }}</td>
                <td>{{ emp.EmployeeEmail }}</td>
                <td>{{ emp.Department }}</td>
                <td>
                    <button type="button" class="btn btn-primary m-2 fload-end" data-bs-toggle="modal"
                        data-bs-target="#exampleModal" @click="edit(emp)">
                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor"
                            class="bi bi-pencil-square" viewBox="0 0 16 16">
                            <path
                                d="M15.502 1.94a.5.5 0 0 1 0 .706L14.459 3.69l-2-2L13.502.646a.5.5 0 0 1 .707 0l1.293 1.293zm-1.75 2.456-2-2L4.939 9.21a.5.5 0 0 0-.121.196l-.805 2.414a.25.25 0 0 0 .316.316l2.414-.805a.5.5 0 0 0 .196-.12l6.813-6.814z" />
                            <path fill-rule="evenodd"
                                d="M1 13.5A1.5 1.5 0 0 0 2.5 15h11a1.5 1.5 0 0 0 1.5-1.5v-6a.5.5 0 0 0-1 0v6a.5.5 0 0 1-.5.5h-11a.5.5 0 0 1-.5-.5v-11a.5.5 0 0 1 .5-.5H9a.5.5 0 0 0 0-1H2.5A1.5 1.5 0 0 0 1 2.5v11z" />
                        </svg>
                    </button>
                    <button type="button" class="btn btn-danger mr-1" @click="remove(emp.EmployeeId)">
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
                                <input type="text" class="form-control" id="floatingInputGrid" v-model="EmployeeName"
                                    placeholder="name">
                                <label for="floatingInputGrid">Employee Name</label>
                            </div>
                        </div>
                        <div class="col-md-6">
                            <div class="form-floating">
                                <input type="text" class="form-control" id="floatingInputGrid" v-model="EmployeePhone"
                                    placeholder="">
                                <label for="floatingInputGrid">Phone</label>
                            </div>
                        </div>
                        <div class="col-md-6">
                            <div class="form-floating">
                                <input type="email" class="form-control" id="floatingInputGrid" v-model="EmployeeEmail"
                                    placeholder="name@example.com">
                                <label for="floatingInputGrid">Email Address</label>
                            </div>
                        </div>
                        <div class="col-md-8">
                            <div class="form-floating">
                                <select class="form-select" id="floatingSelectGrid" v-model="Department"
                                    aria-label="Floating label select example">
                                    <option v-for="dept in departments" :key="dept.id">{{ dept.DepartmentName }}</option>
                                </select>
                                <label for="floatingSelectGrid">Department</label>
                            </div>
                        </div>
                        <div class="col-12">
                            <button type="button" @click="create()" v-if="EmployeeId == 0"
                                class="btn btn-primary">Create</button>
                            <button type="button" @click="update()" v-if="EmployeeId != 0"
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
            departments: [],
            employees: [],
            modalTitle: "",
            EmployeeId: 0,
            EmployeeName: "",
            EmployeePhone: "",
            EmployeeEmail: "",
            Department: "",
        };
    },
    methods: {
        refreshData() {
            axios.get(variable.API_URL + "employee")
                .then((response) => {
                    this.employees = response.data;
                });

            axios.get(variable.API_URL + "department")
                .then((response) => {
                    this.departments = response.data;
                });
        },
        add() {
            this.modalTitle = "Add Employee";
            this.EmployeeId = 0;
            this.EmployeeName = "";
            this.EmployeePhone = "";
            this.EmployeeEmail = "";
            this.Department = "";
        },
        edit(emp) {
            this.modalTitle = "Edit Employee";
            this.EmployeeId = emp.EmployeeId;
            this.EmployeeName = emp.EmployeeName;
            this.EmployeePhone = emp.EmployeePhone;
            this.EmployeeEmail = emp.EmployeeEmail;
            this.Department = emp.Department;
        },
        create() {
            axios.post(variable.API_URL + "employee", {
                EmployeeName: this.EmployeeName,
                EmployeePhone: this.EmployeePhone,
                EmployeeEmail: this.EmployeeEmail,
                Department: this.Department,
            })
                .then((response) => {
                    this.refreshData();
                    alert(response.data);
                });
        },
        update() {
            axios.post(variable.API_URL + "employee/edit/" + this.EmployeeId, {
                EmployeeId: this.EmployeeId,
                EmployeeName: this.EmployeeName,
                EmployeePhone: this.EmployeePhone,
                EmployeeEmail: this.EmployeeEmail,
                Department: this.Department,
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
            axios.post(variable.API_URL + "employee/delete/" + id)
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