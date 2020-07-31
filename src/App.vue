<template>
  <div id="app">
    <ul>   
      <div 
          v-for="item in items[0]" 
          v-bind:key="item.index"
          :style="handleColor(item)"
        >
        <input v-model="item.color" />
        <button>X</button>
      </div>  
      <button>+</button>
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
      return "background-color: " + item.color
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
</style>
