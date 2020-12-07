<template>
  <div class="container">
    <CBox justify-content="center">
      <top-bar @toggle-config-mode="showEditMode = !showEditMode" />
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
            <CEditable default-value="🥵 Sauna" font-size="2xl" width="90%">
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

          {// The new editable one }
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
  CCloseButton,
  CHeading,
  CStack,
  CEditable, CEditableInput, CEditablePreview
} from '@chakra-ui/vue'

export default {
  name: 'App',
  components: {
    CBox,
    CButton,
    CCloseButton,
    CHeading,
    CStack,
    CEditable,
    CEditableInput,
    CEditablePreview
  },
  data () {
    return {
      selectedToBook: null,
      showEditMode: false,
    }
  },
}
</script>
