<template>
  <CBox d="flex" w="100vw" h="10vh" flex-dir="row" justify-content="flex-end">
    <CIconButton
      ml="3"
      right="10px"
      top="10px"
      size="lg"
      icon="minus"
      aria-label="activate edit mode"
      @click="$toggleConfigMode"
    />
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
  computed: {
    colorMode() {
      return this.$chakraColorMode()
    },
  },
  methods: {
    $toggleConfigMode() {
      console.log('asd')
      this.$emit('toggle-config-mode')
    },
    showToast() {
      this.$toast({
        title: 'Dark mode toggled',
        status: 'success',
        duration: 2000,
        isClosable: true,
      })
    },
  },
}
</script>

<style lang="scss" scoped></style>
