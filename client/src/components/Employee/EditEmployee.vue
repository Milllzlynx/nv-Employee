<template>
  <div class="container">
    <h1>Edit Employee</h1>

    <form @submit.prevent="editEmployee">

      <div class="mb-3">
        <label>First Name:</label>
        <input
          type="text"
          v-model="employee.firstName"
          class="form-control">
      </div>

      <div class="mb-3">
        <label>Last Name:</label>
        <input
          type="text"
          v-model="employee.lastName"
          class="form-control">
      </div>

      <div class="mb-3">
        <label>Email:</label>
        <input
          type="email"
          v-model="employee.email"
          class="form-control">
      </div>

      <div class="mb-3">
        <label>Position:</label>
        <input
          type="text"
          v-model="employee.position"
          class="form-control">
      </div>

      <div class="mb-3">
        <label>Salary:</label>
        <input
          type="number"
          v-model="employee.salary"
          class="form-control">
      </div>

      <p>
        <button type="submit">Update Employee</button>
        <button @click="navigateTo('/employees')">
          กลับ
        </button>
      </p>

    </form>
  </div>
</template>

<script>
import EmployeesService from '../../services/EmployeesService'

export default {

  data () {
    return {
      employee: {
        firstName: '',
        lastName: '',
        email: '',
        position: '',
        salary: ''
      }
    }
  },

  async created () {
    try {

      let employeeId = this.$route.params.employeeId

      this.employee = (await EmployeesService.show(employeeId)).data

    } catch (error) {
      console.log(error)
    }
  },

  methods: {

    async editEmployee () {

      try {

        await EmployeesService.put(this.employee)

        this.$router.push({
          name: 'employees'
        })

      } catch (err) {
        console.log(err)
      }

    },

    navigateTo (route) {
      this.$router.push(route)
    }

  }

}
</script>

<style scoped>
</style>