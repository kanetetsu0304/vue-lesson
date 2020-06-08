<template>
  <div class="vue-child" v-if="display">
    <h1 class="vue-child_title">{{ title }}</h1>
    <form @submit.prevent class="item-container">
      <input type="text" v-model="newItem" />
      <button @click="addItem()">Add</button>
    </form>
    <p>{{ `${num}件のタスクがあります` }}</p>
    <ul>
      <li v-for="(todo,index) in todos" :key="todo.id">
        <input type="checkbox" v-model="todo.isDone" />
        <span :class="{done:todo.isDone}">{{ todo.item }}</span>
        <button @click="deleteItem(index)">delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "VueChild",
  props: {
    title: String
  },
  data: function() {
    return {
      newItem: "",
      todos: [],
      display: true
    };
  },
  methods: {
    addItem: function() {
      const todo = {
        item: this.newItem,
        isDone: false
      };
      if (this.newItem === "") {
        return;
      }
      this.todos.push(todo);
      this.newItem = "";
    },
    deleteItem: function(index) {
      this.todos.splice(index, 1);
    }
  },
  computed: {
    num: function() {
      return this.todos.length;
    }
  },
  watch: {
    todos: {
      handler: function() {
        if (this.todos.length === 0) {
          alert(`${this.title}のタスクを全て消化しました！！！`);
        }
      },
      deep: true
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.vue-child {
  width: 200px;
  margin: 0 auto;
}
.vue-child ul {
  list-style: none;
}
.vue-child li > span.done {
  text-decoration: line-through;
}

.vue-child_title {
  text-align: center;
}
.item-container {
  display: flex;
  justify-content: space-between;
}
</style>
