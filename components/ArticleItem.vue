<template>
  <div
    v-if="post"
    :class="[
      featured && 'lg:flex',
      'rounded overflow-hidden shadow-lg mb-4 break-inside-avoid bg-zinc-100 dark:bg-zinc-800',
    ]"
  >
    <NuxtLink :to="'/' + post.slug">
      <nuxt-img
        v-if="post.media"
        :key="post.name"
        class="w-full"
        :src="`/api/assets/${post.media}`"
      />
      <div class="flex flex-col">
        <div class="px-6 py-4 pb-2 flex-1">
          <div class="text-gray-400 mb-2 dark:text-gray-500">{{ date }}</div>
          <div class="font-bold text-xl mb-2 dark:text-white">
            {{ post.name }}
          </div>
          <p class="text-gray-700 text-base dark:text-gray-200">
            {{ post.content }}
          </p>
        </div>
        <div class="px-6 py-4">
          <span
            v-for="(tag, i) in post.tags"
            :key="i"
            class="badge mr-2 dark:text-white"
          >
            #{{ tag }}
          </span>
        </div>
      </div>
    </NuxtLink>
  </div>
</template>

<script>
import dayjs from 'dayjs'

export default {
  props: {
    post: {
      type: Object,
      default: null,
    },
    featured: {
      type: Boolean,
      default: false,
    },
  },
  computed: {
    date() {
      return dayjs(this.post.date_updated ?? this.post.date_created).format(
        'DD MMM YYYY'
      )
    },
  },
}
</script>
