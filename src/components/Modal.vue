<template>
    <!-- Modal -->
    <div class="modal fade" id="exampleModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog" role="document">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title" id="exampleModalLabel">Please edit your info</h5>
                    <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                    <span aria-hidden="true">&times;</span>
                    </button>
                </div>
                <div class="modal-body">
                    <label for="name">Employee Name</label>
                    <input type="text" id="name" class="form-control" v-model="employeeCopy.name">
                    <br>
                    <label for="email">Employee Email</label>
                    <input type="text" id="email" class="form-control" v-model="employeeCopy.email">
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
                    <button type="button" class="btn btn-primary" @click="editEmployee" data-dismiss="modal" id="closemodal">Save changes</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { serverBus } from '../main.js';
import JQuery from 'jquery';
import $ from 'jquery';
export default {
    data() {
        return {
            employeeCopy: {
                name: null,
                email: null
            },
            employee: null
        }
    },
    created() {
        serverBus.$on('employeeSelected', (employee) => {
            this.employee = employee;
            this.employeeCopy.name = this.employee.name
            this.employeeCopy.email = this.employee.email
        });
    },
    methods: {
        editEmployee () {
            window.$ = JQuery
            this.employee.name = this.employeeCopy.name;
            this.employee.email = this.employeeCopy.email;
            const data = {};
            $("#closemodal").on("click", function(e) {
                e.preventDefault(); // prevent de default action, which is to submit
                // save your value where you want
                data.select = $("#exampleModal").value();
                // or call the save function here
                // save();
                $(this).prev().click();
            });
        }
    }
}
</script>