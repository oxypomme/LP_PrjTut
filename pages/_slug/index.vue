<template>
  <div class="mt-5">
    <ArticleDetail :post="post" />
  </div>
</template>

<script>
export default {
  data: () => ({
    post: undefined,
  }),
  async fetch() {
    try {
      const posts = (
        await this.$axios.$get('/items/articles', {
          params: {
            filter: JSON.stringify({ slug: { _eq: this.$route.params.slug } }),
          },
        })
      ).data
      if (posts.length > 0) {
        this.post = posts[0]
      } else {
        this.post = null
      }
    } catch (error) {
      this.posts = { data: [] }
    }
  },
  head: ({ $route }) => ({
    title: 'CIASIE - ' + $route.params.slug,
  }),
}
</script>
