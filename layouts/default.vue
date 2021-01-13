<template>
<div>
  <AppNav />
    <PageBanner pageTitle="Blog v3" />
      <nuxt />
  <TheFooter />
  </div>
</template>

<script>
import AppNav from '~/components/AppNav'
import PageBanner from "~/components/pages/PageBanner";
import TheFooter from '~/components/TheFooter'

export default {
  components: {
    AppNav,
    PageBanner,
    TheFooter
  }
}
</script>

<style>
</style>
