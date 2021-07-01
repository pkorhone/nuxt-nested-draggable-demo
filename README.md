# nuxt-vuedraggable-demo


#### run this to serve app with hot reload at localhost:3000
```
$ npm run dev
```

### Quick explanation
Each instance of ``NestedDraggableList`` component will emit a ``reorder`` event using the ``@end`` event provided by the ``vuedraggable`` package when a drag event for that specific instance ends. The event will include the id of the object that was dragged and originated the event.

This event is handled in the root component ``index.vue`` in the ``onReorder`` function, which takes the id of the dragged element and updates its parent value to the API to match the current front end state.

If ``NestedDraggableList`` receives a ``@reorder`` event emitted by one of its nested child components, we want to pass the id of the dragged child element along with the event, instead of the parent.
We can determine the correct id to pass by evaluating if the emitted value is an original event object or only an id string passed to the function from a nested child component.
