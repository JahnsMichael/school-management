<template>
  <main>
    <Nav />
    <div class="container">
      <breadcrumb />
      <nuxt />
      <Footer />
    </div>
  </main>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Quicksand&display=swap');

* {
  list-style: none;
  text-decoration: none;
  font-family: 'Quicksand', sans-serif;
}

body {
  margin: 0;
}

main {
  display: flex;
  flex-direction: row;
  width: 100%;
  justify-items: stretch;
}

.container {
  margin: 0.5rem;
}

@media (min-width: 600px) {
  .container {
    box-shadow: 0px 0px 20px grey;
    border-radius: 0.5rem;
    margin-left: 0;
    flex-grow: 2;
    padding: 0.5rem;
  }
}
</style>