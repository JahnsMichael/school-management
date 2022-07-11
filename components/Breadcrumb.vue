<template>
  <ol>
    <li v-for="(crumb, index) in crumbs" :key="index">
      <nuxt-link property="item" typeof="WebPage" :to="crumb.path">
        <span property="name">{{ crumb.title }}</span>
      </nuxt-link>
      <meta property="position" :content="index + 2" />
    </li>
  </ol>
</template>

<script>
import * as titleCase from 'ap-style-title-case'

export default {
  computed: {
    crumbs() {
      const fullPath = this.$route.fullPath
      const params = fullPath.startsWith('/')
        ? fullPath.substring(1).split('/')
        : fullPath.split('/')
      const crumbs = []

      let path = ''

      params.forEach((param, index) => {
        path = `${path}/${param}`
        const match = this.$router.match(path)

        if (match.name !== null) {
          crumbs.push({
            title: titleCase(param.replace(/-/g, ' ')),
            ...match,
          })
        }
      })

      return crumbs
    },
  },
}
</script>

<style scoped>
ol {
  list-style: none;
  padding-left: 0;
}

li {
  display: inline;
}

li:after {
  content: ' » ';
  display: inline;
  font-size: 0.9em;
  color: #aaa;
  padding: 0 0.0725em 0 0.15em;
}

li:last-child:after {
  content: '';
}

li a {
  color: black;
}

li a.nuxt-link-exact-active.nuxt-link-active {
  color: grey;
}
</style>