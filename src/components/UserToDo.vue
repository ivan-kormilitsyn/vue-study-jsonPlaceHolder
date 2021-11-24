<template>
  <div id="todos">
    <h1>ToDo:</h1>
    <div v-for="todo in todos" :key="todo.id">
      <div>
        <b-form-checkbox value="accepted" unchecked-value="not_accepted">
          {{ todo.title }}
        </b-form-checkbox>
      </div>

      <!-- 
      1. вывести все(20) ToDo для каждого автора(10) -- сейчас показывает только со значением false 
      2. хочу зачеркивать "выполненые" ToDo
      3. 
       -->
      <!-- <pre>{{ todo.userId }}</pre> -->
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  props: {
    userId: Number,
    completed: Boolean, // сейчас показывает со знач. false
  },

  data() {
    return {
      todos: [],
    };
  },

  async mounted() {
    await this.loadToDos();
  },

  methods: {
    async loadToDos() {
      await axios
        .get("https://jsonplaceholder.typicode.com/todos", {
          params: {
            userId: this.userId,
            completed: this.completed,
          },
        })
        .then((response) => {
          this.todos = response.data;
        });
    },

    // мб попробовать через computed

    //  checkBoxFunction() {
    //     if (this.completed === false) {

    //     }
    //  }
  },
};
</script>