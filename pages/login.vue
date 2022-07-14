<template>
  <div class="login-form-container">
    <h1>Login</h1>
    <form @submit.prevent="userLogin">
      <div>
        <label for="username">Username</label>
        <input
          type="username"
          name="username"
          placeholder="username"
          v-model="login.username"
        />
      </div>
      <div>
        <label for="password">Password</label>
        <input
          type="password"
          name="password"
          placeholder="password"
          v-model="login.password"
        />
      </div>
      <button type="submit">Login</button>
    </form>
    <p class="error">{{ error }}</p>
    <p>
      Doesn't have an account?
      <nuxt-link to="/register">Register now.</nuxt-link>
    </p>
  </div>
</template>

<script>
export default {
  layout: 'login',
  data() {
    return {
      login: {
        username: '',
        password: '',
      },
      error: '',
    }
  },
  methods: {
    async userLogin() {
      try {
        const res = await this.$auth.loginWith('local', { data: this.login })
        if (res.status === 201) {
          this.$router.push({
            path: '/login',
          })
        }
      } catch (err) {
        this.error = err.response.data['detail']
      }
    },
  },
}
</script>

<style scoped>
.login-form-container {
  background-color: white;
  box-shadow: 0px 0px 20px grey;
  padding: 1rem;
  width: 25%;
  min-width: 300px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

input {
  border: none;
  border-radius: 0.5rem;
  padding: 0.5rem 1rem;
  box-shadow: inset 0px 0px 5px grey;
}

form {
  display: flex;
  flex-direction: column;
  width: 80%;
}

form > div {
  margin: 0.5rem;
  display: flex;
  flex-direction: column;
}

form > div > * {
  margin: 0.2rem;
}

button {
  color: white;
  background: rgb(0, 68, 255);
  border: none;
  border-radius: 0.5rem;
  box-shadow: 0px 0px 5px grey;
  padding: 0.5rem;
  margin: 0.7rem;
}

.error {
  color: red;
  font-size: 0.75rem;
}

@media (max-width: 600px) {
  .login-form-container {
    border-radius: 0.5rem;
    margin: 3rem;
    padding: 1rem;
    min-width: none;
  }
}
</style>