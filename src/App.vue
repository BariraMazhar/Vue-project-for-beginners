<template>
  <div id="app">
    <header>
      <nav class="navbar">
      <h1 class="title">TODO LIST</h1>
      </nav>
    </header>
    <div class="container">
      <hr>
      <div class="input">
        <input type="text"
        class="input-form" 
        placeholder="Add item..." 
        v-model="userInput" @keyup.enter="addItem">
        <button class="btn btn-add"
        @click="addItem">ADD</button>
      </div> 
      <div class="todo-list">
        <div class="list-header">
          <h3>To-do list items appear here...</h3>
        </div>
        <div class="list-body">
          <div class="list-row" v-for="(item, index) in filteredList" 
          :key="index" :class="{ 'even-row':
          index % 2 === 0, 'completed': item.completed }">
            <div class="list-item" :class="{ 'completed-cell':
            item.completed }">{{ item.value }}</div>
            <div class="list-item">
              <button class="btn btn-completed"
              @click="toggleCompleted(index)">
                {{ item.completed ? 'Undo' : 'Completed' }}
              </button>
              <button class="btn btn-edit" 
              @click="editItem(index)">Edit</button>
              <button class="btn btn-delete"
              @click="deleteItem(index)">Delete</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      userInput: '',
      searchInput: '',
      list: []
    };
  },
  computed: {
    filteredList() {
      return this.list.filter(item => item.value.toLowerCase()
      .includes(this.searchInput.toLowerCase()));
    }
  },
  methods: {
    addItem() {
      if (this.userInput.trim() !== '') {
        const newItem = {
          id: Math.random(),
          value: this.userInput.trim(),
          completed: false
        };
        this.list.push(newItem);
        this.userInput = '';
      }
    },
    deleteItem(index) {
      this.list.splice(index, 1);
    },
    editItem(index) {
      const editedTodo = prompt('Edit the task:');
      if (editedTodo !== null && editedTodo.trim() !== '') {
        this.list[index].value = editedTodo.trim();
      }
    },
    toggleCompleted(index) {
      this.list[index].completed = !this.list[index].completed;
    }
  }
};
</script>

<style src="./style.css">
</style>


