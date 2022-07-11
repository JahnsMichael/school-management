<template>
  <div class="login-form-container">
    <h1>Register</h1>
    <form>
      <div>
        <label for="email">Email</label>
        <input type="email" name="email" placeholder="email"/>
      </div>
      <div>
        <label for="password">Password</label>
        <input type="password" name="password" placeholder="password"/>
      </div>      
      <div>
        <label for="confirm-password">Confirm Password</label>
        <input type="password" name="confirm-password" placeholder="confirm password"/>
      </div>
      <button>Login</button>
    </form>
    <p>Already have an account? <nuxt-link to="/login">Login now.</nuxt-link></p>
  </div>
</template>

<script>
export default {
  layout: 'login',
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

@media (max-width: 600px) {
  .login-form-container {
    border-radius: 0.5rem;
    margin: 3rem;
    padding: 1rem;
    min-width: none;
  }
}
</style>