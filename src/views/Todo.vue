<template>
  <div>
    <b-card
      bg-variant="dark"
      text-variant="white"
      :title="'Completed Todo Count : ' + count"
      sub-title="Input to do"
      class="m-3"
    >
      <b-form-input placeholder="Enter your todo" @keyup.enter="addTodo"></b-form-input>
      <hr />
      <b-card-text> </b-card-text>

      <a href="#" class="card-link">Card link</a>
      <b-link href="#" class="card-link">Another link</b-link>
    </b-card>
    <b-card bg-variant="light" text-variant="primary" title="◎ 등록된 Todo List" class="m-3">
      <todo-list :todos="todos" @complete-todo="completeTodo" @delete-todo="deleteTodo" />
    </b-card>
  </div>
</template>

<script>
import { defineComponent, ref, computed } from '@vue/composition-api';
import TodoList from '../components/TodoList.vue';

export default defineComponent({
  components: { TodoList },
  setup() {
    const todos = ref([
      { id: Math.random, text: 'study vuejs', checked: false },
      { id: Math.random, text: 'work hard', checked: false },
      { id: Math.random, text: 'do exercise', checked: false }
    ]);
    const count = computed(() => todos.value.filter((todo) => todo.checked).length);
    const completeTodo = ({ e, index }) => {
      todos.value[index].checked = e.target.checked;
    };
    const addTodo = (e) => {
      todos.value.push({
        id: Math.random,
        text: e.target.value,
        checked: false
      });
      e.target.value = '';
    };
    const deleteTodo = (index) => {
      todos.value.splice(index, 1);
    };
    return {
      todos,
      count,
      completeTodo,
      addTodo,
      deleteTodo
    };
  }
});
</script>
