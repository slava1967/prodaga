<template>
  <div>
    <AppNav />
    <nuxt />
    <TheFooter />
  </div>
</template>

<script>
import AppNav from '~/components/AppNav'
import TheFooter from '~/components/TheFooter'

export default {
  components: {
    AppNav,
    TheFooter
  }
}
</script>

<style>
</style>
