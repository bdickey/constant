<template>
  <nav class="main-nav flex-row flex-space-between text-align-center x-pad-single animate__animated animate__fadeInUp animate__faster animate__delay-1s">
    <n-link
      :class="['footer-nav-type h3', !notHome ? 'outline-hover' : 'home-hover']"
      v-for="item of navigation"
      :key="item.slug"
      :to="`/${item.slug}`"
    >
      <span>{{item.name}}</span>
    </n-link>
  </nav>
</template>

<script>
export default {
  name: 'Navigation',
  computed: {
    notHome() {
      return (this.$route.name === "index" || this.$route.name === "about") ? true : false
    },
    navigation() {
      let navItems = []
      this.$global.nav.forEach(item => {
        navItems.push({
          slug: this.$stringToSlug(item),
          name: item
        })
      });
      return navItems
    }
  }
}
</script>

<style lang="css">
  .main-nav {
    height: 100%;
    align-items: center;
    width: 100%;
    position: absolute;
    top: 0;
    left: 0;
    filter: var(--shadow);
    background-color: var(--footer_color);
  }
  .footer-nav-type {
    color: var(--footer_type_color);
    letter-spacing: 1px;
  }
  @media (hover:hover) {
    .home-hover:hover {
      color: var(--pattern_color);
    }
    .home-hover.nuxt-link-exact-active {
      color: var(--pattern_color);
      pointer-events: none;
      -webkit-text-fill-color: var(--white);
      -webkit-text-stroke-color: var(--footer_type_color);
      -webkit-text-stroke-width: 1px;
      -webkit-font-smoothing: antialiased;
    }
    .outline-hover:hover,
    .outline-hover.nuxt-link-exact-active {
      color: transparent;
      -webkit-text-fill-color: transparent;
      -webkit-text-stroke-color: var(--footer_type_color);
      -webkit-text-stroke-width: 1px;
      -webkit-font-smoothing: antialiased;
    }
  }
</style>
