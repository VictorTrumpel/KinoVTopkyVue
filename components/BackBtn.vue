<template>
  <button class="btn btn-outline-info" @click="back">Назад</button>
</template>

<script>
export default {
  name: 'BackBtn',
  methods: {
    back() {
      const url = this.$route.path.split('/')
      url.pop()
      this.$router.push(url.join('/'))
    },
  },
}
</script>

<style scoped></style>
