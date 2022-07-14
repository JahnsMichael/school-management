<template>
  <div>
    <div v-if="error === ''">
      <h1>My Courses</h1>
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
      <h1>All Courses</h1>
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
