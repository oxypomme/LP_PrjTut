<template>
  <div>
    <div class="text-7xl font-bold py-8 dark:text-white">Blog</div>
    <div>
      <ArticleItem featured :post="posts[0]" />
    </div>
    <div class="gap-8 pb-4 columns-1 sm:columns-2 md:columns-3 lg:columns-4">
      <ArticleItem v-for="(post, i) in postsFromSecond" :key="i" :post="post" />
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    posts: [],
  }),
  async fetch() {
    try {
      this.posts = (
        await this.$axios.$get('/items/articles', {
          params: {
            sort: '-date_created',
          },
        })
      ).data
    } catch (error) {
      this.posts = { data: [] }
    }
  },
  computed: {
    postsFromSecond() {
      return this.posts.slice(1)
    },
  },
}
</script>
