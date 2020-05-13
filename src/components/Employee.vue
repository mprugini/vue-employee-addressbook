<template>
    <tbody>
        <tr>
            <td>{{ emp.name }}</td>
            <td>{{ emp.email }}</td>
            <td>
                <button type="button" class="btn btn-success" data-toggle="modal" data-target="#exampleModal" style="margin-right: 10px;" @click="editEmployee">Edit</button>
                <button type="button" class="btn btn-success" @click="deleteEmployee(index)">Delete</button>
            </td>
        </tr>
        <modal :emp="emp"></modal>
    </tbody>
</template>

<script>
import Modal from './Modal';
import { serverBus } from '../main.js';
export default {
    props: ['emp', 'index', 'employees'],
    components: {
        Modal
    },
    methods: {
        deleteEmployee (index) {
            this.employees.splice(index, 1);
            //alert(index);
        },
        editEmployee () {
            //alert('index');
            serverBus.$emit('employeeSelected', this.emp);
        }
    }
}
</script>

