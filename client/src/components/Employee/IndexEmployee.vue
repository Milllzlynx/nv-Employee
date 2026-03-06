<template>
  <div>

    <h2>Get all employees</h2>

    <p>
      <button @click="logout">Logout</button>
    </p>

    <h4>จำนวน employee {{ employees.length }}</h4>

    <p>
      <button @click="navigateTo('/employee/create')">
        สร้าง employee
      </button>
    </p>

    <div v-for="employee in employees" :key="employee.id">

      <p>id: {{ employee.id }}</p>
      <p>First Name: {{ employee.firstName }}</p>
      <p>Last Name: {{ employee.lastName }}</p>
      <p>Email: {{ employee.email }}</p>
      <p>Position: {{ employee.position }}</p>
      <p>Salary: {{ employee.salary }}</p>

      <p>
        <button @click="navigateTo('/employee/' + employee.id)">
          ดู employee
        </button>

        <button @click="navigateTo('/employee/edit/' + employee.id)">
          แก้ไข employee
        </button>

        <button @click="deleteEmployee(employee)">
          ลบข้อมูล
        </button>
      </p>

      <hr>

    </div>

  </div>
</template>

<script>
import EmployeesService from '../../services/EmployeesService'

export default {

  data () {
    return {
      employees: []
    }
  },

  async created () {

    this.employees = (await EmployeesService.index()).data

  },

  methods: {

    logout () {

      this.$store.dispatch('setToken', null)
      this.$store.dispatch('setEmployee', null)

      this.$router.push({
        name: 'login'
      })

    },

    navigateTo (route) {

      this.$router.push(route)

    },

    async deleteEmployee (employee) {

      let result = confirm("Want to delete?")

      if (result) {

        try {

          await EmployeesService.delete(employee)

          this.refreshData()

        } catch (err) {
          console.log(err)
        }

      }

    },

    async refreshData () {

      this.employees = (await EmployeesService.index()).data

    }

  }

}
</script>

<style scoped>
</style>