<template>
  <div>
    <b-navbar toggleable="lg" type="dark" class="navbar">
      <b-navbar-brand href="#">Vikings</b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav class="links">
          <nuxtLink to="/">Home</nuxtLink>
          <nuxtLink to="/cast">Cast</nuxtLink>
          <nuxtLink to="/gallery">Gallery</nuxtLink>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
export default {
  mounted() {
    this.$nextTick(() => {
      this.$nuxt.$loading.start()
      setTimeout(() => this.$nuxt.$loading.finish(), 500)
    })
  },
}
</script>

<style>
.navbar {
  background-color: #7c8f94;
}
.links a {
  padding: 8px 12px;
  margin-right: 10px;
  text-decoration: none;
  background-color: #5a737a;
  color: white;
}
</style>
