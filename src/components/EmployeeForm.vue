<template>
  <div id="employee-form">
    <form v-on:submit.prevent="handleSubmit">
      <label for="employee-name">Employee Name</label>
      <input
        ref="first"
        type="text"
        name="employee-name"
        id="employee-name"
        v-model="employee.name"
        v-bind:class="{ 'has-error': submitting && invalidName }"
        v-on:focus="clearStatus"
        v-on:keypress="clearStatus"
      />

      <label for="employee-email">Employee Email</label>
      <input
        type="text"
        id="employee-email"
        name="employee-email"
        v-model="employee.email"
        v-bind:class="{ 'has-error': submitting && invalidEmail }"
        v-on:focus="clearStatus"
        v-on:keypress="clearStatus"
      />

      <p v-if="error && submitting" class="error-message">
        ❗ Please fill out all required fields
      </p>
      <p v-if="success" class="success-message">
        ✅ Employee successfully added
      </p>

      <button>Add Employee</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "EmployeeForm",
  data() {
    return {
      submitting: false,
      error: false,
      success: false,
      employee: {
        name: "",
        email: "",
      },
    };
  },
  methods: {
    handleSubmit() {
      this.submitting = true;
      this.clearStatus();

      if (this.invalidName || this.invalidEmail) {
        this.error = true;
        return;
      }

      this.$emit("add:employee", this.employee);
      this.employee = {
        name: "",
        email: "",
      };
      // change focus to the first input using is ref
      this.$refs.first.focus();

      this.error = false;
      this.success = true;
      this.submitting = false;
    },

    clearStatus() {
      this.success = false;
      this.error = false;
    },
  },
  computed: {
    invalidName() {
      return this.employee.name === "";
    },
    invalidEmail() {
      return this.employee.email === "";
    },
  },
};
</script>

<style scoped>
form {
  margin-bottom: 2rem;
}

[class*="-message"] {
  font-weight: 500;
}

.error-message {
  color: #d33c40;
}
.success-message {
  color: #32a95d;
}
</style>