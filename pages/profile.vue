<template>
  <div>
    <h1>Profile</h1>
    <p>Name: {{ firstName }} {{ lastName }}</p>
    <p>Username: {{ username }}</p>
    <p>Email: {{ email }}</p>
    <p>Role: {{ group }}</p>
    <nuxt-link to="/login">
      <button>Logout</button>
    </nuxt-link>
  </div>
</template>

<script>
export default {
  name: 'Profile',
  data() {
    return {
      firstName: '',
      lastName: '',
      username: '',
      email: '',
      group: '',
    }
  },
  mounted() {
    this.firstName = this.$auth.user.first_name
    this.lastName = this.$auth.user.last_name
    this.username = this.$auth.user.username
    this.email = this.$auth.user.email

    this.group = this.$auth.user.groups[0] ? this.$auth.user.groups[0].name : 'Not activated yet, please contact the administrator.'
  },
}
</script>

<style scoped>
button {
  background-color: rgb(204, 33, 33);
  color: white;
  border: none;
  border-radius: 0.5rem;
  padding: 1rem;
}
</style>
