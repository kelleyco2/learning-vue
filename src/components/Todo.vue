<template>
    <!-- <div class="todo-main-container"> -->
    <div v-bind:class="[list.items.length ? hasItems : noItems, todoMainContainer]">
        <h1>{{list.title}}</h1>
        <ul v-if="list.items.length">
            <transition-group name="list-transition">
                <li v-for='(item, i) in list.items' v-bind:key="item">
                    {{item}} <button v-on:click="deleteItem(list.id, i)">Delete</button>
                </li>
            </transition-group>
        </ul>
        <div v-else>
            No items currently
        </div>
        New Item: <input v-model="newItem" v-on:keyup.enter="addItem" type="text"><button v-on:click='addItem'>Add Item</button>
        {{newItem}}
    </div>
</template>

<script>
export default {
    name: 'Todo',
    data(){
        return {
            newItem: '',
            todoMainContainer: 'todo-main-container',
            hasItems: 'has-items',
            noItems: 'no-items'
        }
    },
    props: ['list', 'addItemToList', 'deleteItem'],
    methods: {
        addItem(){
            if(this.newItem.length){
                this.addItemToList(this.list.id, this.newItem)
                this.newItem = ''
            }   
        }
    }
}
</script>

<style scoped>
    .todo-main-container{
        width: 300px;
        border: 1px solid black;
        margin: 5px;
    }
    .has-items{
        box-shadow: 3px 3px 3px green;
    }
    .no-items{
        box-shadow: 3px 3px 3px red;
    }
    .list-transition-enter-active, .list-transition-leave-active {
        transition: all 0.5s;
    }   
    .list-transition-enter, .list-transition-leave-to /* .list-leave-active below version 2.1.8 */ {
        opacity: 0;
        /* transform: translateY(30px); */
    }
</style>


