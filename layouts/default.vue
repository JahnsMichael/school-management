<template>
  <main>
    <Nav class="hello" />
    <div class="container">
      <breadcrumb />
      <nuxt />
    </div>
  </main>
</template>

<style scoped>
main {
  display: flex;
  flex-direction: column-reverse;
  width: 100%;
  height: 100vh;
  justify-items: stretch;
}

.container {
  padding: 0.5rem;
  overflow-y: auto;
  flex-grow: 3;
}

@media (min-width: 600px) {
  main {
    flex-direction: row;
  }
}
</style>