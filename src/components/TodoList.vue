
<template>
  <div>
    <h1>ToDoリスト</h1>
    <form>
      <input type="radio" name="state" id="allTodo" checked />
      <label for="allTodo">すべて</label>
      <input type="radio" name="state" id="workingTodo" />
      <label for="workingTodo">作業中</label>
      <input type="radio" name="state" id="doneTodo" />
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
          <tr v-for="(todo,index) in todos" :key="todo.state">
            <td>{{ index }}</td>
            <td>{{ todo.task }}</td>
            <td>
              <button class="state-management-button">{{ todo.state }}</button>
            </td>
            <td>
              <button>削除</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>

    <h2>新規タスクの追加</h2>
    <form>
      <input type="text" class="todoInput" v-model="newTask" />
      <button type="submit" value="追加"  @click="addNewTask">追加</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      todos: []
    };
  },
  methods: {
    addNewTask(e) {
      e.preventDefault();
      if (this.newTask.match(/\S/g)) {
        this.todos.push({ task: this.newTask, state:'作業中'});
      }
      this.newTask = '';
    }
  }
};
</script>

<style scoped>
.state-management-button {
  margin-right:10px;
}

.todoInput {
  margin-right: 10px;
}
</style>

