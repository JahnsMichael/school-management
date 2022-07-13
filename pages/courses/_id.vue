<template>
  <div>
    <div v-if="course.owned">
      <h1>{{ course.name }}</h1>
      <p>{{ course.description }}</p>
      <p>Currently this course has no content yet.</p>
    </div>
    <div v-if="!course.owned">
      <p>
        You don't have access to the class. Please ask your teacher for
        enrollment key or click "request access" to enroll.
      </p>
      <h3>Self Enrollment with Key</h3>
      <form @submit.prevent="enrollWithKey">
        <div>
          <label for="enrollment-key">Enrollment Key</label>
          <input
            type="text"
            name="enrollment-key"
            placeholder="enrollment-key"
            v-model="enrollmentKey"
          />
        </div>
        <button type="submit">Submit Enrollment Key</button>
      </form>
      <h3>Request Access</h3>
      <form @submit.prevent="requestAccess">
        <button type="submit">Request Access</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      course: {
        name: '',
        description: '',
      },
      enrollmentKey: '',
    }
  },
  methods: {
    async enrollWithKey() {
      const res = await this.$axios.post(
        `/enroll-request/bykey/?course-id=${this.$route.params.id}`,
        {
          enrollment_key: this.enrollmentKey,
        }
      )
      if (res.status === 200) {
        this.$router.go()
      }
    },
    async requestAccess() {
      const res = await this.$axios.post(
        `/enroll-request/?course-id=${this.$route.params.id}`)
      if (res.status === 200) {
        this.$router.go()
      }
    },
  },
  async fetch() {
    const res = await this.$axios.get(`/courses/${this.$route.params.id}/`)
    this.course = res.data
  },
}
</script>

<style scoped>
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
</style>