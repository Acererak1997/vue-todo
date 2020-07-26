<template>
  <div>
    <h1>ToDoリスト</h1>
    <label v-for="item in options" :key="item.status">
      <input type="radio" v-model="checked" :value="item.value" />
      {{ item.status }}
    </label>
    <table>
      <thead>
        <tr>
          <th>ID</th>
          <th>タスク</th>
          <th>状態</th>
        </tr>
      </thead>
      <tbody v-for="(todo, index) in filterTodos" :key="todo.id">
        <tr>
          <td>{{ index }}</td>
          <td>{{ todo.task }}</td>
          <td>
            <button @click="changeStatus(todo)">{{ status[todo.status] }}</button>
          </td>
          <td>
            <button @click="deleteTodo(todo)">削除</button>
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
      todos: [],
      options: [
        { value: -1, status: 'すべて'},
        { value: 0, status: '作業中'},
        { value: 1, status: '完了'},
      ],
      checked: -1
    };
  },
  computed: {
    filterTodos : function(){
      return this.todos.filter(function (todo) {
        return this.checked < 0 ? true : this.checked === todo.status
      }, this)
    },
    status() {
      return this.options.reduce(function(a, b) {
        return Object.assign(a, { [b.value]: b.status })
      }, {})
    }
  },
  methods: {
    addTodo: function() {
      if (this.addTask) {
        this.todos.push({
          task: this.addTask,
          status: 0
        });
      }
      this.addTask = "";
    },
    deleteTodo: function(todo) {
      let index = this.todos.indexOf(todo);
      this.todos.splice(index, 1);
    },
    changeStatus: function(todo) {
      todo.status = todo.status ? 0:1
    }
  }
};
</script>
