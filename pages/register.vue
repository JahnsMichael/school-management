<template>
  <div class="login-form-container">
    <h1>Register</h1>
    <form @submit.prevent="userRegister">
      <div>
        <label for="username">Username</label>
        <p class="error" v-for="(err, index) in error.username" :key="index">
          {{ err }}
        </p>
        <input
          type="text"
          name="username"
          placeholder="username"
          v-model="register.username"
        />
      </div>
      <div>
        <label for="password">Password</label>
        <p class="error" v-for="(err, index) in error.password" :key="index">
          {{ err }}
        </p>
        <input
          type="password"
          name="password"
          placeholder="password"
          v-model="register.password"
        />
      </div>
      <div>
        <label for="password_repeat">Repeat Password</label>
        <p class="error" v-for="(err, index) in error.password_repeat" :key="index">
          {{ err }}
        </p>
        <input
          type="password"
          name="password_repeat"
          placeholder="repeat password"
          v-model="register.password_repeat"
        />
      </div>
      <div>
        <label for="first_name">First Name</label>
        <p class="error" v-for="(err, index) in error.first_name" :key="index">
          {{ err }}
        </p>
        <input
          type="text"
          name="first_name"
          placeholder="first_name"
          v-model="register.first_name"
        />
      </div>
      <div>
        <label for="last_name">Last Name</label>
        <p class="error" v-for="(err, index) in error.last_name" :key="index">
          {{ err }}
        </p>
        <input
          type="text"
          name="last_name"
          placeholder="last_name"
          v-model="register.last_name"
        />
      </div>
      <div>
        <label for="email">Email address</label>
        <p class="error" v-for="(err, index) in error.email" :key="index">
          {{ err }}
        </p>
        <input
          type="email"
          name="email"
          placeholder="email"
          v-model="register.email"
        />
      </div>
      <button type="submit">Register</button>
    </form>
    <p>
      Already have an account?
      <nuxt-link to="/login">Login now.</nuxt-link>
    </p>
  </div>
</template>

<script>
export default {
  layout: 'login',
  data() {
    return {
      register: {
        username: '',
        password: '',
        password_repeat: '',
        first_name: '',
        last_name: '',
        email: '',
      },
      error: {},
    }
  },
  methods: {
    async userRegister() {
      try {
        const res = await this.$axios.post('/register/', this.register)
        if (res.status === 201) {
          this.$router.push({
            path: '/login',
          })
        }
      } catch (err) {
        this.error = err.response.data
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
  height: 100vh;
  overflow-y: auto;
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