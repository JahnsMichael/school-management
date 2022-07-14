<template>
  <div>
    <h1>Manage Account</h1>
    <p>Name: {{ account.first_name }} {{ account.last_name }}</p>
    <p>Username: {{ account.username }}</p>
    <p>Email: {{ account.email }}</p>
    <p>
      Role:
      {{ account.groups[0] ? account.groups[0].name : 'Not activated yet.' }}
    </p>
    <form @submit.prevent="changeRole">
      <input type="radio" name="group" value="1" v-model="newGroup" />
      <label for="0">Student</label><br />
      <input type="radio" name="group" value="2" v-model="newGroup" />
      <label for="1">Teacher</label><br />
      <input type="radio" name="group" value="3" v-model="newGroup" />
      <label for="2">Officer</label><br />
      <button type="submit">Change Role</button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'Account',
  data() {
    return {
      account: {
        first_name: '',
        last_name: '',
        username: '',
        email: '',
        groups: [],
      },
      newGroup: null,
    }
  },
  mounted() {
    this.newGroup = this.account.groups[0] ? this.account.groups[0].id : null
  },
  methods: {
    async changeRole() {
      try {
        const res = await this.$axios.patch(
          `/users/${this.$route.params.id}/`,
          {
            groups: [this.newGroup],
          }
        )
        if (res.status === 200) {
          try {
            const res = await this.$axios.get(
              `/users/${this.$route.params.id}/`
            )
            if (res.status === 200) {
              this.account = res.data
            }
          } catch (err) {
            console.log(err.response.data)
          }
        }
      } catch (err) {
        console.log(err)
      }
    },
  },
  async fetch() {
    try {
      const res = await this.$axios.get(`/users/${this.$route.params.id}/`)
      if (res.status === 200) {
        this.account = res.data
      }
    } catch (err) {
      console.log(err.response.data)
    }
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
  margin: 1rem 0;
}
</style>
