<template>
  <div id="app">
    <multi-select-list-mover :selectable-items="SelectableItems" :selected-items="SelectedItems"></multi-select-list-mover>
  </div>
</template>

<script>
import MultiSelectListMover from "./components/MultiSelectListMover.vue";

export default {
  data() {
    return {
      SelectableItems: [
        { uuid: 1, name: "Item 1" },
        { uuid: 2, name: "Item 2" },
        { uuid: 3, name: "Item 3" }
      ],
      SelectedItems: [
        { uuid: 6, name: "Item 6" },
        { uuid: 4, name: "Item 4" },
        { uuid: 5, name: "Item 5" }
      ]
    };
  },
  name: "app",
  components: {
    MultiSelectListMover
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 100%;
  margin: 50px auto;
}
</style>
