<template>
  <Box class="app-info">
    <p class="fs-3 text-uppercase"> all movie : {{ allMoviesCount }}</p>
    <p class="fs-4 text-uppercase"> watched movie : {{ favoriteMoviesCount }}</p>
  </Box>
</template>

<script>
export default {
  props: {
    allMoviesCount: {
      type: Number,
      required: true,
    },
    favoriteMoviesCount: {
      type: Number,
      required: true,
    }
  },
}
</script>


<style scoped>

</style>