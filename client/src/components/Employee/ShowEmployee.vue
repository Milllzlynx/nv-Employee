<template>
  <div>
    <h1>Show Employee</h1>

    <p>id: {{ employee.id }}</p>
    <p>First Name: {{ employee.firstName }}</p>
    <p>Last Name: {{ employee.lastName }}</p>
    <p>Email: {{ employee.email }}</p>
    <p>Position: {{ employee.position }}</p>
    <p>Salary: {{ employee.salary }}</p>

    <p>
      <button @click="navigateTo('/employee/edit/' + employee.id)">
        แก้ไข Employee
      </button>

      <button @click="navigateTo('/employees')">
        กลับ
      </button>
    </p>

  </div>
</template>

<script>
import EmployeesService from '../../services/EmployeesService'

export default {

  data () {
    return {
      employee: null
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
    navigateTo (route) {
      this.$router.push(route)
    }
  }

}
</script>

<style scoped>
</style>