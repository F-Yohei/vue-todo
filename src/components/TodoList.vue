
<template>
  <div>
    <h1>ToDoリスト</h1>
    <form>
      <input type="radio" name="state" id="allTodo" checked v-on:change="allTodo" />
      <label for="allTodo">すべて</label>
      <input type="radio" name="state" id="workingTodo" v-on:change="workingTodo" />
      <label for="workingTodo">作業中</label>
      <input type="radio" name="state" id="doneTodo" v-on:change="doneTodo" />
      <label for="doneTodo">完了</label>
    </form>

    <div>
      <table>
        <thead>
          <tr>
            <th>ID</th>
            <th>コメント</th>
            <th>状態</th>
          </tr>
        </thead>

        <tbody id="todoList">
          <tr v-for="(todo, index) in viewTodos" :key="index">
            <td>{{ todo.id }}</td>
            <td>{{ todo.task }}</td>
            <td>
              <button class="state-management-button" @click="changeState(todo.id)">{{ todo.state }}</button>
            </td>
            <td>
              <button @click="deleteTask(todo.id)">削除</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>

    <h2>新規タスクの追加</h2>
    <form>
      <input type="text" class="todoInput" v-model="newTask" />
      <button type="submit" value="追加" @click="addNewTask">追加</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      todos: [],
      displayState: ''
    };
  },
  computed: {
    viewTodos() {
      return this.displayState
        ? this.todos.filter(todo => todo.state === this.displayState)
        : this.todos;
    }
  },
  methods: {
    //タスクを追加する関数
    addNewTask(e) {
      e.preventDefault();
      if (this.newTask.match(/\S/g)) {
        this.todos.push({
          id: this.todos.length,
          task: this.newTask,
          state: '作業中'
        });
      }
      this.newTask = '';
    },
    //タスクを削除する関数
    deleteTask(id) {
      if (id > -1) {
        this.todos.splice(id, 1);
        this.todos.forEach((todo, index) => {
          todo.id = index;
        });
      }
    },
    //各オブジェクトが保持しているstateの状態を変更する関数
    changeState(id) {
      if (this.todos[id].state === '作業中') {
        this.todos[id].state = '完了';
      } else if (this.todos[id].state === '完了') {
        this.todos[id].state = '作業中';
      }
    },
    //displayStateの状態を作業中に変更する関数
    workingTodo() {
      this.displayState = '作業中';
    },
    //displayStateの状態を完了に変更する関数
    doneTodo() {
      this.displayState = '完了';
    },
    //displayStateの状態を空にする関数
    allTodo() {
      this.displayState = '';
    }
  }
};
</script>


<style scoped>
.state-management-button {
  margin-right: 10px;
}

.todoInput {
  margin-right: 10px;
}
</style>