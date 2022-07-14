<template>
  <div>
    <h1>Manage Account</h1>
    <nuxt-link
      :to="`/accounts/${user.id}`"
      v-for="(user, index) in users"
      :key="index"
    >
      <div class="user-card">
        <h3>{{ user.first_name }} {{ user.last_name }}</h3>
        <p>Username: {{ user.username }}</p>
        <p>Email: {{ user.email }}</p>
        <p>
          Role: {{ user.groups[0] ? user.groups[0].name : 'Not activated yet' }}
        </p>
      </div>
    </nuxt-link>
  </div>
</template>

<script>
export default {
  name: 'Account',
  middleware: 'auth',
  data() {
    return {
      users: [],
    }
  },
  async fetch() {
    try {
      const res = await this.$axios.get('/users/')

      if (res.status === 200) {
        this.users = res.data
      }
    } catch (err) {
      this.error = err.response.data['detail']
    }
  },
  mounted() {
    const group_id = this.$auth.user.groups[0].name
    if (group_id !== 'Officer') {
      this.$router.push({
        path: '/courses',
      })
    }
  },
}
</script>

<style scoped>
.user-card {
  box-shadow: 0px 0px 20px grey;
  border-radius: 0.5rem;
  padding: 1rem;
  margin: 0.5rem;
}
</style>
