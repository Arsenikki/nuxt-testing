<template>
  <CBox d="flex" w="100vw" h="10vh" flex-dir="row" justify-content="flex-end">
    <CIconButton
      ml="3"
      right="10px"
      top="10px"
      size="lg"
      icon="cog"
      :variant-color="configMode ? 'orange' : 'gray'"
      transition="variant-color 0.5s"
      aria-label="activate edit mode"
      @click="$toggleConfigMode"
    >
    </CIconButton>
    <CIconButton
      ml="3"
      right="10px"
      top="10px"
      size="lg"
      :icon="colorMode === 'light' ? 'moon' : 'sun'"
      :aria-label="`Switch to ${colorMode === 'light' ? 'dark' : 'light'} mode`"
      @click="$toggleColorMode"
    />
  </CBox>
</template>

<script>
export default {
  name: 'TopBar',
  inject: ['$chakraColorMode', '$toggleColorMode'],
  data() {
    return {
      configMode: false,
    }
  },
  computed: {
    colorMode() {
      return this.$chakraColorMode()
    },
  },
  methods: {
    $toggleConfigMode() {
      this.$emit('toggle-config-mode')
      this.configMode = !this.configMode
    },
  },
}
</script>

<style lang="scss" scoped></style>
