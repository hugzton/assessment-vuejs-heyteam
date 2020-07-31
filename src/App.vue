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
          <button class="btn-card-delete">X</button>
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
          <button class="btn-card-delete">X</button>
        </div>  
        <button class="btn-card-add" v-on:click="addItem(1, items[1])">+</button>
      </div>
    </ul>
  </div>
</template>okokok

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
      console.log(this.isSelected);
    },
    addItem(id, items) {
        items.push({ list: id, color: "Orange" })
    },
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
  background-color: #f1f1f1;
}

/* Float four columns side by side */
.column {
  float: left;
  width: 25%;
  padding: 0 10px;
}

</style>
