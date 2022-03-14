<template>
  <ArticleList />
</template>

<script>
import ArticleList from '~/components/ArticleList.vue'
export default {
  name: 'IndexPage',
  components: { ArticleList },
  head: () => ({
    title: 'CIASIE Blog',
  }),
}
</script>
