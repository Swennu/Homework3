<template>
  <div class="signup-page">

    <!-- Signup Form -->
    <div class="form-container">
      <form @submit.prevent="handleSignup">
        <div>
          <label>Email</label>
          <input v-model="email" type="email" required />
        </div>

        <div>
          <label>Password</label>
          <input v-model="password" type="password" required />
        </div>

        <button type="submit">Signup</button>

        <!-- Validation Errors -->
        <p v-if="errorMessages.length > 0" class="error">
          The password is not valid:
          <ul>
            <li v-for="(msg, index) in errorMessages" :key="index">{{ msg }}</li>
          </ul>
        </p>
      </form>
    </div>
    </div>
</template>

<script>
export default {
  name: "SignupPage",
  data() {
    return {
      email: "",
      password: "",
      errorMessages: []
    };
  },
  methods: {
    handleSignup() {
      this.errorMessages = this.validatePassword(this.password);

      if (this.errorMessages.length === 0) {
        alert("Signup successful!");
      }
    },

    validatePassword(password) {
      const errors = [];

      if (password.length < 8 || password.length > 15) {
        errors.push("Password must be 8–15 characters long.");
      }

      if (!/^[A-Z]/.test(password)) {
        errors.push("Password must start with an uppercase letter.");
      }

      if (!/[A-Z]/.test(password)) {
        errors.push("Includes at least one uppercase alphabet character.");
      }

      const lowercaseMatches = password.match(/[a-z]/g);
      if (!lowercaseMatches || lowercaseMatches.length < 2) {
        errors.push("Includes at least two lowercase alphabet characters.");
      }

      if (!/[0-9]/.test(password)) {
        errors.push("Includes at least one numeric value.");
      }

      if (!password.includes("_")) {
        errors.push('Password must include the character "_"');
      }

      return errors;
    }
  }
};
</script>

<style scoped>
.signup-page {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.form-container {
  margin: 20px;
  padding: 20px;
  background: #eef4e8;
  border-radius: 10px;
}

form div {
  margin-bottom: 12px;
}

.error {
  margin-top: 10px;
  color: red;
}
</style>