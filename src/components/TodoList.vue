<template>
  <div>
    <div v-for="(todo, index) in reTodos" :key="index">
      <div class="form-check">
        <label class="form-check-label m-1 p-1">
          <input
            type="checkbox"
            class="form-check-input"
            :checked="todo.checked"
            @click="completeTodo($event, index)"
          />
          <span :style="todo.checked ? 'color:gray;text-decoration:line-through' : ''">{{
            todo.text
          }}</span>
        </label>
        <b-button variant="outline-danger" size="sm" v-if="todo.checked" @click="deleteTodo(index)"
          >Delete</b-button
        >
      </div>
    </div>
  </div>
</template>

<script>
import { defineComponent } from '@vue/composition-api';

export default defineComponent({
  props: {
    todos: {
      type: Array,
      require: true
    }
  },
  setup(props, { emit }) {
    const reTodos = props.todos;
    const completeTodo = (e, index) => {
      emit('complete-todo', { e, index });
    };
    const deleteTodo = (index) => {
      emit('delete-todo', index);
    };
    return {
      reTodos,
      completeTodo,
      deleteTodo
    };
  }
});
</script>
