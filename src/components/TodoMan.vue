<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div class="container">
      <div v-for="card in todos" :key="card.title">
        <TodoCard :todo="card" v-on:delete-todo="deleteTodo" ></TodoCard>
      </div>

      <addtodo :todos="todo_titles" :todo="todo_toAdd" @add-todo="addTodo"></addtodo>

      <b-table bordered :items="todos" :fields="todosHeader" head-variant="light">
        <template #cell(detail)="row">
            <b-button @click="row.toggleDetails()">Details</b-button>
        </template>

        <template v-slot:row-details="row">
          <b-table :items="row.item.todos" :fields="subTodosHeader">
          <template #cell(detail)="row">
            <b-button @click="row.toggleDetails()">Details</b-button>
          </template>
          <template v-slot:row-details="row">
            <b-table class="table table-sm" :items="row.item.todos"></b-table>
          </template>
        </b-table>
    </template>

      </b-table>
    </div>
  </div>
</template>

<script>
import Addtodo from './Addtodo.vue';
import TodoCard from './TodoCard.vue';

export default {
  components: { Addtodo, TodoCard },
  name: "TodoMan",
  props: {
    msg: String,
  },
  computed: {
    todo_titles() {
      let titles = [];
      let i;
      for(i =0; i <this.todos.length; i++) {
        titles.push(this.todos[i].title);
      }
      return titles;
    }
  },
  methods: {
    deleteTodo(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.todos.splice(todoIndex, 1);
    },
    toggleDetails() {
      return "row";
    },
    addTodo(newItem) {
      console.log("add todo", newItem);
      let todo = {
        title: newItem.title,
        done: false
      };
      if(newItem.current == undefined)
        this.todos.push(todo);
      else {
        let i;
        for(i=0; i<this.todos.length;i++) {
          if(this.todos[i].title == newItem.current) {
            this.todos[i].todos.push(todo);
            break;
          }
        }
      }
    }
  },
  data: function () {
    return {
      todo_toAdd: {'title' : "new task", 'done': false},
      add_title: "",
      todosHeader: ['title', 'detail', 'done'],
      subTodosHeader: ['title', 'done'],

      todos: [
        {
          title: "Vue.Todo",          
          todos: [
            {
              title: "use npm cli to create vue.todo",              
              done: false,
            },
            {
              title: "add bootstrap, bootstrap-vue into project",              
              done: false,
            },
            {
              title: "link to personal website",              
              done: false,
            },

          ],
          done: false,
        },
        {
          title: "Tooltracker",
          summary: "this is task b",
          todos: [
            {
              title: "b1",              
              done: false,
            },
            {
              title: "b2",              
              done: false,
            },
          ],
          done: false,
        },
      ],
    };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
