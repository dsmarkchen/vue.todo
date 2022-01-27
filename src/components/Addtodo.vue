<template>
  <b-card bg-variant="light" title="Add Todo">
    
        <b-form-group label="Current" label-for="todo-select" label-cols="4" label-cols-lg="2">            
            <v-select
                id="todo-select"
                  :options="todos"
                  v-model="currentTodo"
                  @input="onChangeTodo"
            ></v-select>
        </b-form-group>
        <b-form-group label="New" label-for="todo.title">
            <b-form-input id="todo.title" v-model="todo.title" type="text" v-on:keyup.enter="add" />      
        </b-form-group>
        <b-form-group>
            <b-button v-on:click="add()"> Add </b-button>
        </b-form-group>
    
  </b-card>
</template>

<script>
import vSelect from "vue-select";
import "vue-select/dist/vue-select.css";


export default {
  name: "AddTodo",
  components: {
    vSelect,
  },
  props: {
    todo: Object,
    todos:Array,
  },
  data: function () {
    return {
      count: 0,
      currentTodo: null,
    };
  },
  created: function() {
      
  },
  methods: {
    onChangeTodo() {

    },
    add() {
      this.count++;
      console.log("add???", this.todo);
      this.$emit("add-todo", {
        title: this.todo.title,
        done: this.todo.done,
        current: this.currentTodo
      });
    },
  },
};
</script>

<style scoped>
.bd {
  padding: 1.5rem;
  margin-right: 0;
  margin-left: 0;
  margin-bottom: 0.5rem;
  border-width: 0.2rem;
  border: solid #f9f9f7;
  font-family: "Roboto", arial, sans-serif;
}
</style>
