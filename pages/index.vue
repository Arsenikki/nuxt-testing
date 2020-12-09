<template>
  <div class="container">
    <CBox justify-content="center">
      <top-bar @toggle-config-mode="showEditMode = !showEditMode" />
      <CBox
        d="flex"
        w="100vw"
        h="90vh"
        flex-dir="column"
        align-items="center"
        justify-content="center"
      >
        <CHeading text-align="center" mb="8">
          What do you wanna book?
        </CHeading>
        <item-stack :show-edit-mode="showEditMode" />
      </CBox>
    </CBox>
  </div>
</template>

<script lang="js">
import {
  CBox,
  CHeading,
} from '@chakra-ui/vue'

export default {
  name: 'App',
  components: {
    CBox,
    CHeading,
  },
  data () {
    return {
      showEditMode: false,
    }
  },
  methods: {
    addItem () {
      const arrayOfIDs = this.bookableItems.map((item) => item.id)

      const sortedIDs = arrayOfIDs.sort((a, b) => a - b);
      const missingID = sortedIDs.findIndex((id, index) => id !== index)
      const nextID = missingID !== -1 ? missingID : sortedIDs.length

      this.bookableItems = [
        ...this.bookableItems,
        {
          id: nextID,
          name: ''
        }
      ]
    },
    removeItem(item) {
      const indexToBeDeleted = this.bookableItems.findIndex(object => object === item)
      this.bookableItems.splice(indexToBeDeleted, 1)
    }
  }
}
</script>
