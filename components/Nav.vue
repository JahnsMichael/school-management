<template>
  <div class="navbar">
    <nav>
      <div class="nav-link menu-button">
        <span v-if="isShowing"><x-icon @click="toggleShow"></x-icon></span>
        <span v-if="!isShowing"
          ><menu-icon @click="toggleShow"></menu-icon
        ></span>
        <div class="label" v-if="isShowing">
          <h4>School Management System</h4>
        </div>
      </div>
      <nuxt-link to="/" class="nav-link">
        <span :class="currentlyActive.includes('index') ? 'active' : ''"
          ><home-icon></home-icon
        ></span>
        <div class="label" v-if="isShowing">Home</div>
      </nuxt-link>
      <nuxt-link to="/my-course" class="nav-link">
        <span :class="currentlyActive.includes('my-course') ? 'active' : ''"
          ><book-icon></book-icon
        ></span>
        <div class="label" v-if="isShowing">My Course</div>
      </nuxt-link>
      <nuxt-link to="/profile" class="nav-link end">
        <span :class="currentlyActive.includes('profile') ? 'active' : ''"
          ><user-icon></user-icon
        ></span>
        <div class="label" v-if="isShowing">Profile</div>
      </nuxt-link>
    </nav>
  </div>
</template>

<script>
import {
  HomeIcon,
  UserIcon,
  BookIcon,
  XIcon,
  MenuIcon,
} from 'vue-feather-icons'

export default {
  data() {
    return {
      isShowing: false,
      currentlyActive: 'index',
    }
  },
  methods: {
    toggleShow() {
      this.isShowing = !this.isShowing
    },
  },
  watch: {
    $route() {
      this.currentlyActive = this.$route.name
    },
  },
  mounted() {
    this.currentlyActive = this.$route.name
  },
  components: {
    HomeIcon,
    UserIcon,
    BookIcon,
    XIcon,
    MenuIcon,
  },
}
</script>

<style scoped>
.navbar {
  height: 100vh;
  max-width: 100%;
  display: flex;
}

nav {
  padding: 0.2rem 1rem;
  background: rgb(0, 68, 255);
  box-shadow: 0px 0px 20px grey;
  display: flex;
  flex-direction: column;
  box-sizing: border-box;
  flex-grow: 2;
}

nav > * {
  color: white;
}

.nav-link {
  display: flex;
  align-items: center;
  margin: 0.5rem 0;
}

.label {
  margin-left: 0.5rem;
}

.end {
  margin-top: auto;
}

h4 {
  margin-block: 0;
}

span {
  padding: 0.25rem 0.35rem;
  border-radius: 0.5rem;
}

.active {
  background: rgb(255, 208, 0);
}

.active > * {
  color: black;
}

@media (max-width: 600px) {
  .navbar {
    display: block;
    height: fit-content;
    flex-grow: 0;
  }

  nav {
    height: fit-content;
    flex-direction: row;
    justify-content: space-around;
    padding: 1rem;
  }

  .label {
    display: none;
  }

  .nav-link {
    margin: 0;
  }

  .menu-button {
    display: none;
  }
}
</style>