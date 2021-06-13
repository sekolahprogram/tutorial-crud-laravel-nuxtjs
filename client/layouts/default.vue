<template>
  <div>
    <nav class="navbar has-shadow">
      <div class="container">
        <div class="navbar-brand">
          <NuxtLink to="/" class="navbar-item">Home</NuxtLink>
          <a
            @click="isNavbar = !isNavbar"
            :class="['navbar-burger', {
              'is-active': isNavbar
            }]"
          >
            <span aria-hidden="true"></span>
            <span aria-hidden="true"></span>
            <span aria-hidden="true"></span>
          </a>
        </div>
        <div
          :class="['navbar-menu', {
            'is-active': isNavbar
          }]"
        >
          <div class="navbar-end">
            <NuxtLink :to="{ name: 'users' }" class="navbar-item is-tab">Users</NuxtLink>
          </div>
        </div>
      </div>
    </nav>

    <section class="section">
      <div class="container">
        <Nuxt />
      </div>
    </section>

    <footer class="footer">
      <div class="content has-text-centered">
        <p>
          <strong>&copy;2021 Febri Hidayan</strong>
        </p>
      </div>
    </footer>
    
  </div>
</template>

<script>
export default {
  data() {
    return {
      isNavbar: false
    }
  }
}
</script>