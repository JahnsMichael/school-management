<template>
  <div class="card">
    <div class="title">
      <h3>{{ title }}</h3>
      <h4>{{ author }}</h4>
    </div>
    <p>{{ description }}</p>
  </div>
</template>

<script>
export default {
  props: {
    title: String,
    description: String,
    author: String,
  },
}
</script>

<style scoped>
.card {
  box-shadow: 0px 0px 20px grey;
  border-radius: 0.5rem;
  padding: 1rem;
  margin: 0.5rem;
}

.title {
  display: flex;
  justify-content: space-between;
}
</style>