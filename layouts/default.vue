<template>
  <main>
    <Nav class="hello" />
    <div class="container">
      <breadcrumb />
      <nuxt />
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

::-webkit-scrollbar {
  width: 5px;
}

::-webkit-scrollbar-track {
  background: white;
}

::-webkit-scrollbar-thumb {
  background: rgb(0, 68, 255);
  border-radius: 10px;
}

::-webkit-scrollbar-thumb:hover {
  background: rgb(0, 68, 255);
}

main {
  display: flex;
  flex-direction: column-reverse;
  width: 100%;
  height: 100vh;
  justify-items: stretch;
}

.container {
  margin: 0.5rem;
  margin-bottom: 0rem;
  box-shadow: 0px 0px 20px grey;
  border-radius: 0.5rem;
  padding: 0.5rem;
  overflow-y: auto;
  flex-grow: 3;
}

@media (min-width: 600px) {
  .container {
    margin: 0.5rem;
    margin-left: 0;
  }

  main {
    flex-direction: row;
  }
}
</style>