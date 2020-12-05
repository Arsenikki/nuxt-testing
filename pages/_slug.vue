<template>
  <div>
    <nuxt-content :document="doc" />
    <h1>{{ doc.bestBeer }}</h1>
  </div>
</template>

<script>
export default {
  async asyncData({ $content, params }) {
    const doc = await $content(params.slug || 'index').fetch()
    return { doc }
  },
}
</script>

<style lang="scss" scoped></style>
