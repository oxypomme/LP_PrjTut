<template>
  <div class="max-w-sm rounded overflow-hidden shadow-lg mb-4 break-inside">
    <nuxt-img
      v-if="post.media"
      :key="post.name"
      class="w-full"
      :src="`/api/assets/${post.media}`"
    />
    <div class="px-6 py-4 pb-2">
      <div class="font-bold text-xl mb-2">{{ post.name }}</div>
      <p class="text-gray-700 text-base">
        {{ post.content }}
      </p>
    </div>
    <div class="px-6 py-4">
      <span v-for="(tag, i) in post.tags" :key="i" class="badge mr-2">
        #{{ tag }}
      </span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    post: {
      type: Object,
      required: true,
    },
  },
}
</script>

<style lang="postcss" scoped>
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer utilities {
  @variants responsive {
    .break-inside {
      break-inside: avoid;
    }
  }
}
</style>
