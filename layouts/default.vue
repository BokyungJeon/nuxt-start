<template>
  <div>
    <header class="title">
      <nuxt-link class="logo" to="/">Nuxt Shopping</nuxt-link>
      <!-- <h1><NuxtLink to="/">Nuxt Shopping</NuxtLink></h1> -->
      <!-- <h1>{{ $route.name }}페이지</h1>
      <NuxtLink to="/">홈페이지</NuxtLink>
      <NuxtLink to="/main">메인페이지</NuxtLink>
      <NuxtLink to="/product">상품페이지</NuxtLink> -->
    </header>
    <Nuxt />
  </div>
</template>

<script>
export default {}
</script>

<style>
header {
  height: 60px;
  display: flex;
  align-items: center;
  padding: 0 0.5rem;
}

.logo {
  font-weight: 900;
}

.logo:visited {
  color: inherit;
}
</style>
