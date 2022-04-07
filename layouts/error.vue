<template>
  <ErrorAlert type="danger" :title="title" :message="message" />
</template>

<script>
export default {
  layout: 'default',
  props: ['error'],
  computed: {
    title() {
      if (this.error.statusCode === 404) {
        return 'Content not found'
      }
      return 'An error occured'
    },
    message() {
      if (this.error.statusCode === 404) {
        return 'Content not found'
      }
      return 'Please contact developers ASAP'
    },
  },
}
</script>
