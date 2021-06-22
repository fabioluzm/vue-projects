<template>
  <div id="employee-table">
    <p v-if="employees.length < 1">No employees to show!</p>
    <table v-else>
      <thead>
        <tr>
          <th>Employee Name</th>
          <th>Employee Email</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="employee in employees" v-bind:key="employee.id">
          <td>{{ employee.name }}</td>
          <td>{{ employee.email }}</td>
          <td>
            <button @click="$emit('update:employee', employee.id)">Edit</button>
            <button v-on:click="$emit('delete:employee', employee.id)">
              Delete
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "EmployeeTable",
  props: {
    employees: Array,
  },
};
</script>

<style scoped>
button {
  margin: 0 0.5rem 0 0;
}

button:nth-of-type(1) {
  background-color: blue;
  border-color: blue;
}
button:nth-of-type(2) {
  background-color: #d33c40;
  border-color: #d33c40;
}
button:nth-of-type(1):hover {
  opacity: 0.75;
}
button:nth-of-type(2):hover {
  opacity: 0.9;
}
</style>