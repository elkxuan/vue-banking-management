<template>
    <div class="d-flex justify-content-between align-items-center">
        <div>
            <h1>View Department</h1>
        </div>
    </div>
    <div class="d-flex justify-content-end">
        <button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#exampleModal" @click="add()">
            Add Department
        </button>
    </div>
    <table class="table table-striped table-hover">
        <thead>
            <tr>
                <th>
                    <!-- <div class="d-flex flex-row">
                        <input class="form-control m-2" v-model="DepartmentIdFilter" v-on:keyup="FilterFn()"
                            placeholder="Filter by Department ID">
                        <button type="button" class="btn btn-light" @click="sortResult('DepartmentId', true)">
                            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor"
                                class="bi bi-arrow-down-square" viewBox="0 0 16 16">
                                <path fill-rule="evenodd"
                                    d="M15 2a1 1 0 0 0-1-1H2a1 1 0 0 0-1 1v12a1 1 0 0 0 1 1h12a1 1 0 0 0 1-1V2zM0 2a2 2 0 0 1 2-2h12a2 2 0 0 1 2 2v12a2 2 0 0 1-2 2H2a2 2 0 0 1-2-2V2zm8.5 2.5a.5.5 0 0 0-1 0v5.793L5.354 8.146a.5.5 0 1 0-.708.708l3 3a.5.5 0 0 0 .708 0l3-3a.5.5 0 0 0-.708-.708L8.5 10.293V4.5z" />
                            </svg>
                        </button>

                        <button type="button" class="btn btn-light" @click="sortResult('DepartmentId', false)">
                            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor"
                                class="bi bi-arrow-up-square" viewBox="0 0 16 16">
                                <path fill-rule="evenodd"
                                    d="M15 2a1 1 0 0 0-1-1H2a1 1 0 0 0-1 1v12a1 1 0 0 0 1 1h12a1 1 0 0 0 1-1V2zM0 2a2 2 0 0 1 2-2h12a2 2 0 0 1 2 2v12a2 2 0 0 1-2 2H2a2 2 0 0 1-2-2V2zm8.5 9.5a.5.5 0 0 1-1 0V5.707L5.354 7.854a.5.5 0 1 1-.708-.708l3-3a.5.5 0 0 1 .708 0l3 3a.5.5 0 0 1-.708.708L8.5 5.707V11.5z" />
                            </svg>
                        </button>
                    </div> -->
                    Department ID
                </th>
                <th>
                    <!-- <div class="d-flex flex-row">
                        <input class="form-control m-2" v-model="DepartmentNameFilter" v-on:keyup="FilterFn()"
                            placeholder="Filter by Department Name">
                        <button type="button" class="btn btn-light" @click="sortResult('DepartmentName', true)">
                            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor"
                                class="bi bi-arrow-down-square" viewBox="0 0 16 16">
                                <path fill-rule="evenodd"
                                    d="M15 2a1 1 0 0 0-1-1H2a1 1 0 0 0-1 1v12a1 1 0 0 0 1 1h12a1 1 0 0 0 1-1V2zM0 2a2 2 0 0 1 2-2h12a2 2 0 0 1 2 2v12a2 2 0 0 1-2 2H2a2 2 0 0 1-2-2V2zm8.5 2.5a.5.5 0 0 0-1 0v5.793L5.354 8.146a.5.5 0 1 0-.708.708l3 3a.5.5 0 0 0 .708 0l3-3a.5.5 0 0 0-.708-.708L8.5 10.293V4.5z" />
                            </svg>
                        </button>

                        <button type="button" class="btn btn-light" @click="sortResult('DepartmentName', false)">
                            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor"
                                class="bi bi-arrow-up-square" viewBox="0 0 16 16">
                                <path fill-rule="evenodd"
                                    d="M15 2a1 1 0 0 0-1-1H2a1 1 0 0 0-1 1v12a1 1 0 0 0 1 1h12a1 1 0 0 0 1-1V2zM0 2a2 2 0 0 1 2-2h12a2 2 0 0 1 2 2v12a2 2 0 0 1-2 2H2a2 2 0 0 1-2-2V2zm8.5 9.5a.5.5 0 0 1-1 0V5.707L5.354 7.854a.5.5 0 1 1-.708-.708l3-3a.5.5 0 0 1 .708 0l3 3a.5.5 0 0 1-.708.708L8.5 5.707V11.5z" />
                            </svg>
                        </button>
                    </div> -->
                    Department Name
                </th>
                <th>Number of Employees</th>
                <th>Action</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="dept in departments" :key="dept.id">
                <td>{{ dept.DepartmentId }}</td>
                <td>{{ dept.DepartmentName }}</td>
                <td>{{ departmentEmployeeCount[dept.DepartmentName] || 0 }}</td>
                <td>
                    <button type="button" class="btn btn-primary m-2 fload-end" data-bs-toggle="modal"
                        data-bs-target="#exampleModal" @click="edit(dept)">
                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor"
                            class="bi bi-pencil-square" viewBox="0 0 16 16">
                            <path
                                d="M15.502 1.94a.5.5 0 0 1 0 .706L14.459 3.69l-2-2L13.502.646a.5.5 0 0 1 .707 0l1.293 1.293zm-1.75 2.456-2-2L4.939 9.21a.5.5 0 0 0-.121.196l-.805 2.414a.25.25 0 0 0 .316.316l2.414-.805a.5.5 0 0 0 .196-.12l6.813-6.814z" />
                            <path fill-rule="evenodd"
                                d="M1 13.5A1.5 1.5 0 0 0 2.5 15h11a1.5 1.5 0 0 0 1.5-1.5v-6a.5.5 0 0 0-1 0v6a.5.5 0 0 1-.5.5h-11a.5.5 0 0 1-.5-.5v-11a.5.5 0 0 1 .5-.5H9a.5.5 0 0 0 0-1H2.5A1.5 1.5 0 0 0 1 2.5v11z" />
                        </svg>
                    </button>
                    <button type="button" class="btn btn-danger mr-1" @click="remove(dept.DepartmentId)">
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

    <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true"
        ref="departmentModal">
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
                                <input type="text" class="form-control" id="floatingInputGrid" v-model="DepartmentName"
                                    placeholder="name">
                                <label for="floatingInputGrid">Department Name</label>
                            </div>
                        </div>
                        <div class="col-12">
                            <button type="button" @click="create()" v-if="DepartmentId == 0"
                                class="btn btn-primary">Create</button>
                            <button type="button" @click="update()" v-if="DepartmentId != 0"
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
            modalTitle: "",
            DepartmentName: "",
            DepartmentId: 0,
            DepartmentIdFilter: "",
            DepartmentNameFilter: "",
            departmentsWithoutFilter: [],
            departmentEmployeeCount: {}
        };
    },
    methods: {
        refreshData() {
            axios.get(variable.API_URL + "employee")
                .then((response) => {
                    this.employees = response.data;
                    this.departmentEmployeeCount = {};
                    for (const emp of this.employees) {
                        const departmentName = emp.Department;
                        if (!this.departmentEmployeeCount[departmentName]) {
                            this.departmentEmployeeCount[departmentName] = 1;
                        } else {
                            this.departmentEmployeeCount[departmentName]++;
                        }
                    }
                });

            axios.get(variable.API_URL + "department")
                .then((response) => {
                    this.departments = response.data;
                    this.departmentsWithoutFilter = response.data;
                });
        },
        add() {
            this.modalTitle = "Add Department";
            this.DepartmentId = 0;
            this.DepartmentName = "";
        },
        edit(dept) {
            this.modalTitle = "Edit Department";
            this.DepartmentId = dept.DepartmentId;
            this.DepartmentName = dept.DepartmentName;
        },
        create() {
            axios.post(variable.API_URL + "department", {
                DepartmentName: this.DepartmentName
            })
                .then((response) => {
                    this.refreshData();
                    alert(response.data);
                });
        },
        update() {
            axios.post(variable.API_URL + "department/edit/" + this.DepartmentId, {
                DepartmentId: this.DepartmentId,
                DepartmentName: this.DepartmentName
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
            axios.post(variable.API_URL + "department/delete/" + id)
                .then((response) => {
                    this.refreshData();
                    alert(response.data);
                });
        },
        FilterFn() {
            var DepartmentIdFilter = this.DepartmentIdFilter;
            var DepartmentNameFilter = this.DepartmentNameFilter;

            this.departments = this.departmentsWithoutFilter.filter(
                function (el) {
                    return el.DepartmentId.toString().toLowerCase().includes(
                        DepartmentIdFilter.toString().trim().toLowerCase()
                    ) &&
                        el.DepartmentName.toString().toLowerCase().includes(
                            DepartmentNameFilter.toString().trim().toLowerCase()
                        )
                });
        },
        sortResult(prop, asc) {
            this.departments = this.departmentsWithoutFilter.sort(function (a, b) {
                if (asc) {
                    return (a[prop] > b[prop]) ? 1 : ((a[prop] < b[prop]) ? - 1 : 0);
                }
                else {
                    return (b[prop] > a[prop]) ? 1 : ((b[prop] < a[prop]) ? - 1 : 0);
                }
            });
        }
    },
    created() {
        this.refreshData();
    }
}
</script>