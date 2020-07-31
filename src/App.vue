<template>
  <div id="app">
    <ul>
      <div class="list">
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
        <button class="btn-list-add" v-on:click="addItem(0, items[0])">+</button>
      </div>
    </ul>
    <div class="column">
      <button v-on:click="moveItem()">MOVE</button>
      <button v-on:click="deleteSelectItem()">DELETE</button>
      <button v-on:click="copyItem()">COPY</button>
      <button v-on:click="refItem()">REFERENCE</button>
      
    </div>
    <ul>
      <div class="list">
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
        <button class="btn-list-add" v-on:click="addItem(1, items[1])">+</button>
      </div>
    </ul>
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
      let overlay = "";
      if (item == this.isSelected) {
        overlay = "border: 2px solid WhiteSmoke;"
      }
      return overlay + "background-color: " + item.color
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
      if (this.isSelected != null) {
        this.items[this.isSelected.list].splice(this.items[this.isSelected.list].indexOf(this.isSelected), 1);
        this.isSelected = null
      }
    },
    copyItem() {
      if (this.isSelected != null){
        this.items[this.isSelected.list].push({
          list: this.isSelected.list,
          color: this.isSelected.color
        })
        this.isSelected = null
      }
    },
    refItem(){
      if (this.isSelected != null && this.items[this.isSelected.list].length < 6) {
        let ref = this.isSelected
        this.items[this.isSelected.list].push(ref)
      }
    },
    moveItem() {
      if (this.isSelected != null && this.isSelected.list == 0 && this.items[1].length < 6) {
        this.isSelected.list = 1;
        this.items[1].push(this.isSelected);
        this.items[0].splice(this.items[0].indexOf(this.isSelected), 1);
      } else if (this.isSelected != null && this.items[0].length < 6 ) {
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
  margin-top: 100px;
}

.list {
  display: flex;
  flex-flow: row wrap;
  justify-content: left;
  padding: 0;
  margin: 0;
  border: 1px solid black;
  background-color: grey;
}

.btn-card-delete {
  top:0; 
  right:0;
  z-index :1;
}

.btn-list-add {
  top:0; 
  right:0;
  z-index :1;
}

#itm {
  position: relative;
}

.card {
  padding: 5px;
  width: 200px;
  height: 150px;
  margin: 10px;
  line-height: 150px;
  color: white;
  font-weight: bold;
  font-size: 3em;
  text-align: center;
}

/* Float four columns side by side */
.column {
  display: flex;
  justify-content: center;
  flex-direction: column;
  background: grey;
}

</style>
