<template>
  <b-card bg-variant="light" :title="todo.title"   
    tag="article"    
    class="mb-2">
    {{ todo.done }}

    <b-table bordered :items="todo.todos" :fields="todosHeader" head-variant="light">
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

    <span class='right floated edit icon' v-on:click="showForm">
        <i class='edit icon'></i> edit
    </span>
    
    <span class='right floated trash icon' v-on:click="deleteTodo(todo)">
        <i class='trash icon'></i> delete
    </span>
  </b-card>
</template>

<script>
export default {
  name: "TodoCard",
  props: {
    todo: Object,
  },
  methods: {
    deleteTodo(todo) {
        console.log(todo);
         this.$emit('delete-todo', todo);
    },
    showForm() {

    }
  },
  data: function () {
    return {
      todosHeader: ["title", "detail", "done"],
      subTodosHeader: ["title", "done"],
    };
  },
};
</script>

<style scoped></style>
