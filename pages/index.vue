<template>
  <div class="container">
    <CBox v-bind="mainStyles[colorMode]" justify-content="center">
      <CBox
        d="flex"
        w="100vw"
        h="10vh"
        flex-dir="row"
        justify-content="flex-end"
      >
        <CIconButton
          ml="3"
          right="10px"
          top="10px"
          size="lg"
          icon="minus"
          aria-label="activate edit mode"
          @click="showEditMode = !showEditMode"
        />
        <CIconButton
          ml="3"
          right="10px"
          top="10px"
          size="lg"
          :icon="colorMode === 'light' ? 'moon' : 'sun'"
          :aria-label="`Switch to ${
            colorMode === 'light' ? 'dark' : 'light'
          } mode`"
          @click="
            toggleColorMode()
            showToast()
          "
        />
      </CBox>

      <CBox
        d="flex"
        w="100vw"
        h="90vh"
        flex-dir="column"
        justify-content="center"
      >
        <CHeading text-align="center" mb="8">
          What do you wanna book?
        </CHeading>
        <CStack :spacing="3">
          <CButton
            d="flex"
            align-items="center"
            justify-content="space-between"
            py="8"
            mx="10vw"
            shadow="md"
            border-radius="full"
            border-width="1px"
          >
            <CEditable
              default-value="🥵 Sauna"
              font-size="2xl"
              placeholder="yolo kappa"
              width="90%"
            >
              <CEditablePreview />
              <CEditableInput />
            </CEditable>
            <CCloseButton v-if="showEditMode" border-radius="full" size="lg" />
          </CButton>
          <CButton
            d="flex"
            align-items="center"
            justify-content="space-between"
            py="8"
            mx="10vw"
            shadow="md"
            border-radius="full"
            border-width="1px"
          >
            <CEditable
              default-value="🧺 Laundry"
              font-size="2xl"
              width="90%"
              my="6"
            >
              <CEditablePreview />
              <CEditableInput />
            </CEditable>
            <CCloseButton v-if="showEditMode" border-radius="full" size="lg" />
          </CButton>

          {// last one }
          <CButton
            d="flex"
            align-items="center"
            justify-content="space-between"
            py="8"
            mx="10vw"
            shadow="md"
            border-radius="full"
            border-width="1px"
          >
            <CEditable font-size="2xl" width="90%" my="6">
              <CEditablePreview />
              <CEditableInput />
            </CEditable>
            <CCloseButton v-if="showEditMode" border-radius="full" size="lg" />
          </CButton>
        </CStack>
      </CBox>
    </CBox>
  </div>
</template>

<script lang="js">
import {
  CBox,
  CButton,
  CIconButton,
  CCloseButton,
  CFlex,
  CHeading,
  CStack,
  CEditable, CEditableInput, CEditablePreview
} from '@chakra-ui/vue'

export default {
  name: 'App',
  inject: ['$chakraColorMode', '$toggleColorMode'],
  components: {
    CBox,
    CButton,
    CCloseButton,
    CIconButton,
    CFlex,
    CHeading,
    CStack,
    CEditable, CEditableInput, CEditablePreview
  },
  data () {
    return {
      selectedToBook: null,
      showEditMode: false,
      mainStyles: {
        dark: {
          bg: 'gray.700',
          color: 'whiteAlpha.900'
        },
        light: {
          bg: 'white',
          color: 'gray.900'
        },
      }
    }
  },
  computed: {
    colorMode () {
      return this.$chakraColorMode()
    },
    theme () {
      return this.$chakraTheme()
    },
    toggleColorMode () {
      return this.$toggleColorMode
    },
  },
  methods: {
    showToast () {
      this.$toast({
        title: 'Dark mode toggled',
        status: 'success',
        duration: 2000,
        isClosable: true
      })
    }
  }
}
</script>
