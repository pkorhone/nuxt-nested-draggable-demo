<template>
  <nested-draggable-list :items="itemList" @reorder="onReorder" />
</template>

<script>
import _ from 'lodash';
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
  itemListBeforeReorder = [];  // we can compare itemList to this after a drag event to find differences that should be updated to the API

  mounted() {
    this.itemListBeforeReorder = _.cloneDeep(this.itemList);
  }

  onReorder(itemId) {
    console.log('Dragged item id:', itemId)
    console.log('itemList structure before reorder:', this.itemListBeforeReorder);
    console.log('Current itemList structure:', this.itemList);

    // ... compare current structure to previous and send updates to API

    // update itemListBeforeReorder to current state
    this.itemListBeforeReorder = _.cloneDeep(this.itemList);
  }
}
</script>
