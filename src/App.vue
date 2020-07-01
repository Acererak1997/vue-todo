<template>
  <div>
    <h1>ToDoリスト</h1>
    <form>
      <input type="radio" value="すべて" />すべて
      <input type="radio" value="作業中" />作業中
      <input type="radio" value="完了" />完了
    </form>
    <table>
      <thead>
        <tr>
          <th>ID</th>
          <th>タスク</th>
          <th>状態</th>
        </tr>
      </thead>
      <tbody v-for="(todo, index) in todos" :key="todo.id">
        <tr>
          <td>{{ index }}</td>
          <td>{{ todo.task }}</td>
          <td>
            <button>{{ todo.status }}</button>
          </td>
          <td>
            <button>削除</button>
          </td>
        </tr>
      </tbody>
    </table>
    <form>
      <input type="text" placeholder="add To Do" v-model="addTask" />
      <button @click.prevent="addTodo">追加</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      addTask: "",
      todos: [
      ]
    };
  },
  methods: {
    addTodo: function(){
      if(this.addTask){
        this.todos.push({
          task: this.addTask,
          status: "作業中"
        });
      }
      this.addTask= "";
    }
  }
};
</script>
