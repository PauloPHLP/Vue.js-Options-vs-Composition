<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <h3>You have {{ todosCount }} todos!</h3>

    <div>
      <input type="text" placeholder="Add a todo" v-model="data.newTodoName" @keyup.enter="addTodo">
    </div>
    <div>
      <ul>
        <li v-for="(todo, index) in data.todos" :key="todo.id">
          <span>{{ todo.name }}</span>
          <button @click="deleteTodo(index)">X</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import {
  reactive, computed, watch,
} from 'vue';

export default {
  setup() {
    const data = reactive({
      newTodoName: '',
      todos: [],
    });

    const swearWords = [
      'fart',
      'butt hair',
      'willy',
    ];
    const todosCount = computed(() => data.todos.length);

    function addTodo() {
      const newTodo = {
        id: Date.now(),
        name: data.newTodoName,
      };

      data.todos.push(newTodo);
      data.newTodoName = '';
    }

    function deleteTodo(index) {
      data.todos.splice(index, 1);
    }

    watch(data, (newValue) => {
      if (swearWords.includes(newValue.newTodoName.toLowerCase())) {
        alert(`You must NEVER say ${newValue.newTodoName}`);
        data.newTodoName = '';
      }
    });

    return {
      data,
      todosCount,
      addTodo,
      deleteTodo,
    };
  },
};
</script>

<style>
ul {
  list-style: none;
  padding: 0;
  width: 200px;
  margin: 20px auto 0;
}

li {
  border: 1px solid;
  display: flex;
  margin-bottom: 10px;
}

li span {
  flex-grow: 1;
}
</style>
