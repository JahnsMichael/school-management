<template>
  <div>
    <h1>Create a New Course</h1>
    <form @submit.prevent="createNewCourse">
      <div>
        <label for="name">Course Name</label>
        <input type="text" name="name" id="name" v-model="course.name"/><br />
      </div>
      <div>
        <label for="description">Description</label><br />
        <textarea name="" id="" cols="30" rows="10" v-model="course.description"></textarea><br />
      </div>
      <div>
        <label for="enrollment_key">Enrollment Key</label>
        <input type="text" name="enrollment_key" id="enrollment_key" v-model="course.enrollment_key"/><br />
      </div>
      <button type="submit">Create</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      course: {
        name: '',
        description: '',
        enrollment_key: '',
      },
    }
  },
  methods: {
    async createNewCourse() {
      try {
        const res = await this.$axios.post('/courses/', this.course)

        if (res.status === 201) {
          this.$router.push({
            path: '/courses',
          })
        }
      } catch (error) {}
    },
  },
}
</script>

<style scoped>
input, textarea {
  border: none;
  border-radius: 0.5rem;
  padding: 0.5rem 1rem;
  box-shadow: inset 0px 0px 5px grey;
}

form {
  display: flex;
  flex-direction: column;
}

form > div {
  margin: 0.4rem;
  display: flex;
  flex-direction: column;
}

form > div > * {
  margin: 0.1rem;
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