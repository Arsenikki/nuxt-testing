<template>
  <CStack :spacing="3" align="center" width="full">
    <CButton
      v-for="item in bookableItems"
      :key="item.id"
      d="flex"
      width="80%"
      py="8"
      shadow="md"
      border-radius="full"
      border-width="1px"
      :aria-label="`book ${item.name}`"
    >
      <CEditable
        :is-preview-focusable="showEditMode ? true : false"
        :default-value="item.name"
        font-size="2xl"
        width="65%"
      >
        <CEditablePreview />
        <CEditableInput />
      </CEditable>

      <CIconButton
        v-if="showEditMode"
        right="2"
        variant="ghost"
        variant-color="gray"
        position="absolute"
        border-radius="full"
        size="lg"
        icon="close"
        mt="2px"
        aria-label="add more items"
        @click="removeItem(item)"
      />
    </CButton>

    {ADD-button shown in edit mode}
    <CIconButton
      v-if="showEditMode"
      width="50px"
      align-items="center"
      justify-content="center"
      py="8"
      mx="10vw"
      variant-color="gray"
      shadow="md"
      border-radius="full"
      border-width="1px"
      size="lg"
      icon="add"
      aria-label="add item"
      @click="addItem"
    />
  </CStack>
</template>

<script>
export default {
  name: 'ItemStack',
  props: {
    showEditMode: Boolean,
  },
  data() {
    return {
      bookableItems: [
        {
          id: 0,
          name: '🧺 Laundry',
        },
        {
          id: 4,
          name: '🥵 Sauna',
        },
      ],
    }
  },
  methods: {
    addItem() {
      const arrayOfIDs = this.bookableItems.map((item) => item.id)

      const sortedIDs = arrayOfIDs.sort((a, b) => a - b)
      const missingID = sortedIDs.findIndex((id, index) => id !== index)
      const nextID = missingID !== -1 ? missingID : sortedIDs.length

      this.bookableItems = [
        ...this.bookableItems,
        {
          id: nextID,
          name: '',
        },
      ]
    },
    removeItem(item) {
      const indexToBeDeleted = this.bookableItems.findIndex(
        (object) => object === item
      )
      this.bookableItems.splice(indexToBeDeleted, 1)
    },
  },
}
</script>

<style lang="scss" scoped></style>
