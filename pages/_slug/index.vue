<template>
  <div class="mt-5">
    <ArticleDetail v-if="post !== null" :post="post" />
    <ErrorAlert
      v-else
      title="Content not found"
      message="The content that you're asking for is unavailable."
    />
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
        throw new Error('Content not found')
      }
    } catch (error) {
      this.post = null
    }
  },
  head() {
    const name = this.post?.name ?? this.$route.params.slug
    return {
      title: 'CIASIE - ' + name,
    }
  },
}
</script>
