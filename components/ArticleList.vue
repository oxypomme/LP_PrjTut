<template>
  <div class="masonry sm:masonry-sm md:masonry-md">
    <ArticleItem v-for="post in posts.data" :key="post.id" :post="post" />
  </div>
</template>

<script>
export default {
  data: () => ({
    posts: {
      data: [],
    },
  }),
  async fetch() {
    try {
      this.posts = await this.$axios.$get('/items/articles')
    } catch (error) {
      this.posts = { data: [] }
    }
  },
}
</script>

<style lang="postcss" scoped>
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer utilities {
  @variants responsive {
    .masonry {
      column-gap: 1.5em;
      column-count: 1;
    }
    .masonry-sm {
      column-gap: 1.5em;
      column-count: 2;
    }
    .masonry-md {
      column-gap: 1.5em;
      column-count: 3;
    }
  }
}
</style>
