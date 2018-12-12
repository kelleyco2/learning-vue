<template>
  <div id="app">
    {{greeting}} {{timeOfDay}}
    <Todo v-for="list in lists" v-bind:key="list.id" :list='list' :addItemToList='addItemToList' :deleteItem='deleteItem'></Todo>
    <div class="todo-main-container">test</div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import Todo from './components/Todo.vue'

export default {
  name: 'app',
  components: {
    HelloWorld,
    Todo
  },
  mounted(){
    this.timeIntervalId = setInterval(() => {
      this.timeOfDay = new Date().toLocaleString()
    }, 1000);
  },
  data(){
    return {
      lists: [
        {
          id: 1,
          items: ['get stuff', 'register', 'finish book'],
          title: 'my day'
        },
        {
          id: 2,
          items: ['foo1', 'food2', 'food 3'],
          title: 'food'
        },
        {
          id: 3,
          items: ['stuff 1', 'stuff 2', 'stuff 3'],
          title: 'stuff'
        }
      ],
      timeIntervalId: 0,
      timeOfDay: new Date().toLocaleString(),
      firstName: 'Cooper'
    }
  },
  methods: {
    addItemToList(id, newItem){
      for(let i = 0; i < this.lists.length; i++){
        if(this.lists[i].id === id){
          this.lists[i].items.push(newItem)
        } 
      }
    },
    deleteItem(id, itemIndex){
      for(let i = 0; i < this.lists.length; i++){
        if(this.lists[i].id === id){
          this.lists[i].items.splice(itemIndex, 1)
        }
      }
    }
  },
  computed: {
    greeting(){
      return `Hello ${this.firstName}, the time and date right now is`
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
