<template>
  <div>
    <div v-if="error === ''">
      <h1>My Courses</h1>
      <p v-if="ownedCourses.length === 0">You don't have any courses. Please enroll from the available course in the "All Courses" section.</p>
      <nuxt-link
        v-for="(course, index) in ownedCourses"
        :key="`ownedCourses-${index}`"
        :to="`/courses/${course.id}/`"
      >
        <course-card
          :title="course.name"
          :author="`${course.author.first_name} ${course.author.last_name}`"
          :description="course.description"
        />
      </nuxt-link>
      <nuxt-link v-if="this.$auth.user.groups && this.$auth.user.groups[0].name === 'Teacher'" class="new-courses-btn" to="/courses/new">+ Create New Courses</nuxt-link>
      <h1>All Courses</h1>
      <p v-if="allCourses.length === 0">There are no available course yet.</p>
      <nuxt-link
        v-for="(course, index) in allCourses"
        :key="`allCourses-${index}`"
        :to="`/courses/${course.id}/`"
      >
        <course-card
          :title="course.name"
          :author="`${course.author.first_name} ${course.author.last_name}`"
          :description="course.description"
        />
      </nuxt-link>
    </div>
    <div v-if="error !== ''">
      <h1>Opps, your account is not activated</h1>
      <p>
        Currently your account is not activated yet. Please contact the
        administrator.
      </p>
    </div>
  </div>
</template>

<script>
import CourseCard from '~/components/CourseCard.vue'
export default {
  components: { CourseCard },
  name: 'MyCourse',
  middleware: 'auth',
  data() {
    return {
      allCourses: [],
      ownedCourses: [],
      error: '',
    }
  },
  async fetch() {
    try {
      const res_courses = await this.$axios.get('/courses/')
      const res_courses_owned = await this.$axios.get('/courses/owned/')

      if (res_courses.status === 200) {
        this.allCourses = res_courses.data
      }

      if (res_courses_owned.status === 200) {
        this.ownedCourses = res_courses_owned.data
      }
    } catch (err) {
      this.error = err.response.data['detail']
    }
  },
}
</script>