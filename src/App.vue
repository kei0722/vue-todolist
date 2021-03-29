<template>
  <div class="container">
    <h2>ToDoリスト</h2>
    <div class="show-area">
      <input type="radio" id="all" value="all" v-model="chosen" />
      <label for="all">すべて</label>
      <input type="radio" id="doing" value="doing" v-model="chosen" />
      <label for="doing">作業中</label>
      <input type="radio" id="done" value="done" v-model="chosen" />
      <label for="done">完了</label>
      <table>
        <thead>
          <tr>
            <th>ID</th>
            <th>コメント</th>
            <th>状態</th>
            <th></th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(todo, index) in filteredTodos" :key="index">
            <td>{{ index }}</td>
            <td>{{ todo.item }}</td>
            <td>
              <button @click="todo.isDone = !todo.isDone">
                <span v-if="!todo.isDone">作業中</span>
                <span v-else>完了</span>
              </button>
            </td>
            <td><button @click="deleteItem(index)">削除</button></td>
          </tr>
        </tbody>
      </table>
    </div>
    <div class="input-area">
      <h2>新規タスクの追加</h2>
      <input type="text" v-model="newItem" />
      <button class="add-btn" @click="addItem">追加</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      chosen: 'all',
      newItem: '',
      todos: [],
    };
  },
  computed: {
    filteredTodos() {
      return this.todos.filter((todo) => {
        if (this.chosen === 'all') {
          return this.todos;
        } else if (this.chosen === 'doing') {
          return todo.isDone === false;
        } else if (this.chosen === 'done') {
          return todo.isDone === true;
        }
      });
    },
  },
  methods: {
    addItem() {
      const todo = {
        item: this.newItem,
        isDone: false,
      };
      if (this.newItem === '') return;
      this.todos.push(todo);
      this.newItem = '';
    },
    deleteItem(index) {
      this.todos.splice(index, 1);
    },
  },
};
</script>

<style>
.add-btn {
  margin-left: 10px;
}
</style>
