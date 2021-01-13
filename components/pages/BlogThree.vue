<template>
  <section class="commonSection blogPage">
    <div class="container">
      <div class="row">
        <div class="col-lg-8 col-sm-8">
          <div class="row">
            <div class="col-lg-6 col-sm-12 col-md-6">
              <div class="latestBlogItem">
                <div class="lbi_details">
                  <ul v-if="posts.length">
                    <li v-for="post in posts" :key="post.id">

                      <Post :post="post" />

                    </li>
                  </ul>
                  <div v-else>no posts</div>

                  <Pagination
                    :routeRootName="'category-slug'"
                    :routeName="'category-slug-page-id'"
                    :routeSlug="this.pageSlug"
                    :pageNumber="1"
                    :totalPages="this.totalPages" />
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="col-lg-4 col-sm-4 sidebar">
          <aside class="widget categories">
            <h3 class="widget_title">Categories</h3>
            <div class="meipaly_categorie_widget">
              <ul>
                <li class="menu__item" v-for="category in categories" :key="category.id">
                  <n-link class="menu--link" :to="{ name: 'category-slug', params: { slug: category.slug }}">
                    {{ category.name }}
                  </n-link>
                </li>
              </ul>
            </div>
          </aside>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import Pagination from '~/components/AppPagination'
import Post from '~/components/Post'
import { mapGetters } from 'vuex'

export default {
  async asyncData( { store, params, route, error } ) {
    const catId = store.getters['categories/getId']((route.params.slug))

    // if the category ID does not exist, I tag the page with 404
    if ( catId ) {
      await store.dispatch('posts/category/getCategoryPosts', {
        slug: route.params.slug,
        categoryId: catId,
        pageId: 1
      })
    } else {
      error({ statusCode: 404, message: 'Category not found' })
    }
  },
  components: {
    Pagination,
    Post
  },
  head() {
    return {
      title: this.categoryTitle,
      titleTemplate: null,
      bodyAttrs: {
        class: `archive category category-${this.caregoryId} category-${this.pageSlug}`
      },
      meta: [
        { hid: 'description', name: 'description', content: '' }
      ]
    }
  },
  name: "categorySlug",
  
  data() {
    return {
      pageSlug: this.$route.params.slug
    }
  },
  computed: {
    posts() {
      return this.$store.getters['posts/category/get']({
        id: 1,
        name: this.pageSlug
      })
    },
    caregoryId() {
      return this.$store.getters['categories/getId']((this.pageSlug))
    },
    totalPages() {
      return Number( this.$store.getters['posts/category/totalPages'](this.pageSlug) )
    },
    categoryTitle() {
      return this.$store.getters['categories/getTitle']((this.pageSlug))
    },
    categories() {
       return this.$store.getters['categories/get']
    }
  },
}
</script>

<style scoped>
</style>