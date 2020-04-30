<template>
  <h2 class="text-center">
    {{ word }}
  </h2>
</template>

<script>
export default {
  name: 'current-word',
  props: {
    word: String
  }
}
</script>

<style lang="scss" scoped></style>
