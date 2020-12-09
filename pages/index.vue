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
            v-for="item in bookableItems"
            :key="item.id"
            :todo="item"
            d="flex"
            align-items="center"
            justify-content="space-between"
            py="8"
            mx="10vw"
            shadow="md"
            border-radius="full"
            border-width="1px"
          >
            <CEditable :default-value="item.name" font-size="2xl" width="90%">
              <CEditablePreview />
              <CEditableInput />
            </CEditable>

            <CCloseButton
              v-if="showEditMode"
              border-radius="full"
              size="lg"
              @click="removeItem(item)"
            />
          </CButton>
          {// The new editable one }
          <CButton
            v-if="showEditMode"
            d="flex"
            align-items="center"
            justify-content="space-between"
            py="8"
            mx="10vw"
            shadow="md"
            border-radius="full"
            border-width="1px"
          >
            <CEditable font-size="4xl" width="90%" my="6" @submit="addItem">
              <CEditablePreview />
              <CEditableInput />
            </CEditable>
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
      bookableItems: [
        {
          id: 0,
          name: "🧺 Laundry"
        },
        {
          id: 4,
          name: "🥵 Sauna"
        }
      ],
      showEditMode: false,
    }
  },
  methods: {
    addItem (value) {
      if (value !== '') {
        const arrayOfIDs = this.bookableItems.map((item) => item.id)

        const sortedIDs = arrayOfIDs.sort((a, b) => a - b);
        const missingID = sortedIDs.findIndex((id, index) => id !== index)
        const nextID = missingID !== -1 ? missingID : sortedIDs.length

        this.bookableItems.push(
          {
            id: nextID,
            name: value
          }
        )
      }
    },
    removeItem(item) {
      const indexToBeDeleted = this.bookableItems.findIndex(object => object === item)
      this.bookableItems.splice(indexToBeDeleted, 1)
    }
  }
}
</script>
