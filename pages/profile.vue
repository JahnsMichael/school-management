<template>
  <div>
    <h1>Profile</h1>
    <p>Name: {{ firstName }} {{ lastName }}</p>
    <p>Username: {{ username }}</p>
    <p>Email: {{ email }}</p>
    <p>Role: {{ group }}</p>
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

    const group_id = this.$auth.user.groups[0]
    if (group_id === 1) {
      this.group = 'Student'
    } else if (group_id === 2) {
      this.group = 'Teacher'
    } else if (group_id === 3) {
      this.group = 'Officer'
    } else {
      this.group = ''
    }
  },
}
</script>
