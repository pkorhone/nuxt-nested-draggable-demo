<template>
  <draggable
    class="draggable-class"
    tag="ul"
    :animation="200"
    :group="{ name: 'g1' }"
    :list="items"
    @end="onEnd($event, $event.item._underlying_vm_.id)"
  >
    <li v-for="item in items" :key="item.id">
      <h2>{{ item.title }}</h2>
      <nested-draggable-list :items="item.children" @reorder="onEnd($event)" />
    </li>
  </draggable>
</template>

<script>
import {  Component, Emit, Prop, Vue } from 'nuxt-property-decorator';
import draggable from 'vuedraggable';

@Component({
  components: { draggable }
})
export default class NestedDraggableList extends Vue {
  @Prop() items

  @Emit('reorder')
  onEnd(event, eventId) {
    // if the received event parameter is already a string, we know it is an id passed to this component by a nested child and we can just emit the same string value.
    // if the received event parameter is an actual event call by this instance, we need to instead emit the eventId parameter.
    return typeof event === 'string' ? event : eventId
  }
}
</script>

<style lang="css">
.draggable-class {
  border: 1px solid;
  min-height: 40px;
  margin-bottom: 30px;
}
</style>
