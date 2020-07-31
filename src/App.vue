<template>
  <div id="app">
    <ul>
      <div class="column">
        <div
            class="card"
            v-for="item in items[0]" 
            v-bind:key="item.index"
            :style="handleColor(item)"
            v-on:click="handleSelect(item)"
          >
          <input style=" width: 25%;" v-model="item.color" />
          <button class="btn-card-delete" v-on:click="deleteItem(items[0], item)">X</button>
        </div>  
        <button class="btn-card-add" v-on:click="addItem(0, items[0])">+</button>
      </div>
    </ul>
    <ul>
      <div class="column">   
        <div 
            class="card"
            v-for="item in items[1]" 
            v-bind:key="item.index"
            :style="handleColor(item)"
            v-on:click="handleSelect(item)"
          >
          <input style=" width: 25%;" v-model="item.color" />
          <button class="btn-card-delete" v-on:click="deleteItem(items[1], item)">X</button>
        </div>  
        <button class="btn-card-add" v-on:click="addItem(1, items[1])">+</button>
      </div>
    </ul>
    <button v-on:click="moveItem()">MOVE</button>
    <button v-on:click="copyItem()">COPY</button>
    <button v-on:click="refItem()">REFERENCE</button>
    <button v-on:click="deleteSelectItem()">DELETE</button>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      isSelected: null,
      items: [
        [
          {
            list: 0,
            color: "Orange"
          },
          {
            list: 0,
            color: "Blue"
          },
        ],
        [
          {
            list: 1,
            color: "Orange"
          },
          {
            list: 1,
            color: "Blue"
          },
        ]
      ]
    }
  },
  
  methods: {
    handleColor (item) {
      return "background-color: " + item.color
    },
    handleSelect (item) {
      this.isSelected = item
    },
    addItem(id, items) {
        if (this.items[id].length < 6) {
          items.push({ list: id, color: "Orange" })
        }
    },
    deleteItem(items, item) {
      items.splice(items.indexOf(item), 1);
    },
    deleteSelectItem() {
      this.items[this.isSelected.list].splice(this.items[this.isSelected.list].indexOf(this.isSelected), 1);
      this.isSelected = null
    },
    copyItem() {
      this.items[this.isSelected.list].push({
        list: this.isSelected.list,
        color: this.isSelected.color
      })
      this.isSelected = null
    },
    refItem(){
      let ref = this.isSelected
      this.items[this.isSelected.list].push(ref)
    },
    moveItem() {
      if (this.isSelected.list == 0 && this.items[1].length < 6) {
        this.isSelected.list = 1;
        this.items[1].push(this.isSelected);
        this.items[0].splice(this.items[0].indexOf(this.isSelected), 1);
      } else if (this.items[0].length < 6) {
        this.isSelected.list = 0;
        this.items[0].push(this.isSelected);
        this.items[1].splice(this.items[1].indexOf(this.isSelected), 1);
      }
      this.isSelected = null
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.list {
  border: 1px solid black;
}
.btn-card-delete {
  top:0; 
  right:0;
  z-index :1;
}

.btn-card-add {
  top:0; 
  right:0;
  z-index :1;
}

#itm {
  position: relative;
}

.card {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  padding: 16px;
  text-align: center;
}

/* Float four columns side by side */
.column {
  float: left;
  width: 25%;
  padding: 0 10px;
}

</style>
