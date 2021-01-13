<template>
  <section class="pageBanner">
    <div class="container">
      <div class="row">
        <div class="col-lg-12">
          <div class="banner_content text-center">
            <h4><nuxt-link to="/">home</nuxt-link> - {{ pageTitle }}</h4>
            <h2>{{ pageTitle }}</h2>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
    export default {
      name: "PageBanner",
      props: {
        pageTitle: {
          type: String
        }
      }
    }
</script>

<style scoped>
.pageBanner {
    position: relative;
    min-height: 465px;
    background:
    linear-gradient(
      rgba(0, 0, 0, 0.5), 
      rgba(0, 0, 0, 0.5)
    ),
    url(/images/bg/8.jpg) no-repeat center center / cover;
    padding-top: 224px;
}
</style>
