<template>
  <div class="template">
    <div class="container">
      <div class="layout">
        <div class="header selectable">Selectable Items</div>
        <input type="text" placeholder="Search" v-model="selectableSearch">
        <ul>
          <li
            v-for="(item,uuid) in filteredSelectableItems"
            :key="uuid"
            :data-uuid="item.uuid"
            @click="select(item)"
          >{{item.name}}</li>
        </ul>
        <div class="buttons">
          <button @click="selectAll" class="btn select">Select All</button>
        </div>
      </div>
      <div class="arrows">
        <i class="material-icons">keyboard_arrow_right</i>
        <i class="material-icons">keyboard_arrow_left</i>
      </div>
      <div class="layout">
        <div class="header selected">Selected Items</div>
        <input type="text" placeholder="Search" v-model="selectedSearch">
        <ul>
          <li
            v-for="(item,uuid) in filteredSelectedItems"
            :key="uuid"
            :data-uuid="item.uuid"
            @click="deselect(item)"
          >{{item.name}}</li>
        </ul>
        <div class="buttons">
          <button @click="deselectAll" class="btn deselect">Deselect All</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "MultiSelectListMover",
  props: {
    SelectableItems: { type: Array, required: true, default: [] },
    SelectedItems: { type: Array, required: true, default: [] }
  },
  data() {
    return {
      selectableSearch: "",
      selectedSearch: ""
    };
  },
  computed: {
    filteredSelectedItems() {
      return this.SelectedItems.filter(item => {
        return item.name
          .toLowerCase()
          .includes(this.selectedSearch.toLowerCase());
      });
    },
    filteredSelectableItems() {
      return this.SelectableItems.filter(item => {
        return item.name
          .toLowerCase()
          .includes(this.selectableSearch.toLowerCase());
      });
    }
  },
  methods: {
    select(item) {
      let index = this.SelectableItems.indexOf(item);
      this.SelectableItems.splice(index, 1);
      this.SelectedItems.push(item);
    },
    deselect(item) {
      let index = this.SelectedItems.indexOf(item);
      this.SelectedItems.splice(index, 1);
      this.SelectableItems.push(item);
    },
    selectAll() {
      this.SelectableItems.forEach(item => {
        this.SelectedItems.push(item);
      });
      this.SelectableItems.splice(0, this.SelectableItems.length);
    },
    deselectAll() {
      this.SelectedItems.forEach(item => {
        this.SelectableItems.push(item);
      });
      this.SelectedItems.splice(0, this.SelectedItems.length);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
  display: flex;
  text-align: center;
  font-family: "Roboto", sans-serif;
}
ul {
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  transition: border linear 0.2s, box-shadow linear 0.2s;
  border: 1px solid #ccc;
  -webkit-border-radius: 3px;
  -moz-border-radius: 3px;
  border-radius: 3px;
  height: 200px;
  padding: 0;
  overflow-y: auto;
  margin: 0;
  width: 250px;
}
li {
  border-bottom: 1px #eee solid;
  padding: 5px;
  color: #555;
  font-size: 15px;
}
li:hover {
  background: #08c;
}
.header {
  border: gray 1px solid;
  font-weight: bold;
  font-size: 14px;
  padding: 10px;
  border-radius: 3px;
}
.header.selectable {
  background-color: blue;
  color: white;
}
.header.selected {
  background-color: red;
  color: white;
}

input {
  width: 250px;
  margin: 5px auto;
  padding: 5px;
  border-radius: 3px;
  border: lightgray 2px solid;
  box-sizing: border-box;
}
input:focus {
  border: skyblue 2px solid;
  outline: none;
}
.arrows {
  margin-top: 120px;
  height: 60px;
}
.arrows i {
  font-size: 30px;
  display: block;
}
.buttons {
  margin: 5px auto;
}
.buttons .btn {
  padding: 5px;
  box-sizing: border-box;
  width: 100%;
}
.btn.select {
  background: white;
  color: blue;
  border: blue 1px solid;
  box-shadow: gray 1px 1px 5px;
  font-family: inherit;
  cursor: pointer;
  border-radius: 3px;
}
.btn.select:hover {
  background: blue;
  color: white;
  border: blue 1px solid;
}
.btn.deselect {
  background: white;
  color: red;
  border: red 1px solid;
  box-shadow: gray 1px 1px 5px;
  font-family: inherit;
  cursor: pointer;
  border-radius: 3px;
}
.btn.deselect:hover {
  background: red;
  color: white;
  border: red 1px solid;
}
</style>
