<template>
  <div>
    <h1>My Courses</h1>
    <nuxt-link v-for="(course, index) in ownedCourses" :key="`ownedCourses-${index}`" :to="`/courses/${course.id}/`">
      <course-card
        :title="course.name"
        :author="`${course.author.first_name} ${course.author.last_name}`"
        :description="course.description"
      />
    </nuxt-link>
    <h1>All Courses</h1>
    <nuxt-link v-for="(course, index) in allCourses" :key="`allCourses-${index}`" :to="`/courses/${course.id}/`">
      <course-card
        :title="course.name"
        :author="`${course.author.first_name} ${course.author.last_name}`"
        :description="course.description"
      />
    </nuxt-link>
  </div>
</template>

<script>
import CourseCard from '~/components/CourseCard.vue'
export default {
  components: { CourseCard },
  name: 'MyCourse',
  middleware: 'auth',
  async asyncData({ $axios }) {
    let [allCourses, ownedCourses] = await Promise.all([
      await $axios.get('/courses/'),
      await $axios.get('/courses/owned/'),
    ])

    return {
      allCourses: allCourses.data,
      ownedCourses: ownedCourses.data,
    }
  },
}
</script>
