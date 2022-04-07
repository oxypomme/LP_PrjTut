<template>
  <div v-if="post">
    <div class="w-full rounded overflow-hidden" style="max-height: 35vh">
      <nuxt-img
        v-if="post.media"
        :key="post.name"
        class="w-full"
        :src="`/api/assets/${post.media}`"
      />
    </div>
    <div class="flex flex-col">
      <div class="px-6 py-4 pb-2 flex-1">
        <div class="font-bold text-6xl mb-2 dark:text-white">
          {{ post.name }}
        </div>
        <div class="text-gray-400 mb-2 dark:text-gray-500">{{ date }}</div>
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
  </div>
</template>

<script>
import dayjs from 'dayjs'

export default {
  props: {
    post: {
      type: Object,
      required: false,
      default: undefined,
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
