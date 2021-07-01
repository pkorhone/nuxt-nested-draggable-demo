<template>
  <nested-draggable-list :items="itemList" @reorder="onReorder" />
</template>

<script>
import { Component, Vue } from 'nuxt-property-decorator';
import NestedDraggableList from '~/components/NestedDraggableList.vue';

@Component({
  components: { NestedDraggableList }
})
export default class IndexPage extends Vue {
  itemList = [
    { title: '1', id: 1, children: [] },
    { title: '2', id: 2, children: [
        { title: '3', id: 3, children: [] },
        { title: '4', id: 4, children: [] }
      ] }
  ]

  onReorder(itemId) {
    console.log('Dragged item id:', itemId)
  }
}
</script>
