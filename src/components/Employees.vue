<template>
    <div>
        <div class="row">
            <div class="col-sm-6">
                <div class="form-group">
                    <label for="name">Employee Name</label>
                    <input type="text" id="name" class="form-control" v-model="name">
                </div>
                <div class="form-group">
                    <label for="email">Employee Email</label>
                    <input type="text" id="email" class="form-control" v-model="email">
                </div>
                <button type="button" class="btn btn-success" @click="addEmployee">Add Employee</button>
            </div>
        </div>
        <br>
        <div class="row" v-if="employees.length !== 0">
            <div class="col-sm-6">
                <table class="table">
                    <thead>
                        <tr>
                            <th scope="col">Name</th>
                            <th scope="col">Email</th>
                            <th scope="col">Edit/Delete</th>
                        </tr>
                    </thead>
                    <employee v-for="(emp, index) in employees" :emp="emp" :index="index" :employees="employees" v-bind:key="(emp, index)"></employee>
                </table>
            </div>
        </div>
    </div>
</template>

<script>
import Employee from './Employee';
import 'vuejs-noty/dist/vuejs-noty.css'
export default {
    components: {
        Employee
    },
    data () {
        return {
            name: '',
            email: '',
            employees: []
        }
    },
    methods: {
        addEmployee () {
            //alert(this.employee);
            const emp = {
                name: this.name,
                email: this.email
            }
            if (emp.name === '' || emp.email === '') {
                //alert('You cant add empty fields')
                this.$noty.error("Oops, something went wrong!")
            } else {
                this.employees.push(emp);
            }
        }
    }
}
</script>
