<!-- .vue 파일은 3가지로 이루어져 있음 --> 

<!-- html 코드가 들어감 -->
<template>
  <div class="container">
    <h2>To-Do List</h2>
    <form 
      @submit.prevent="onSubmit"
      class="d-flex"
    >
      <div class="flex-grow-1 mr-2">
        <input 
          class="form-control" 
          type="text" 
          v-model="todo" 
          placeholder="Type new to-do"
        >
      </div>
      <div>
        <button 
          class="btn btn-primary" 
          type="submit"
        > 
          Add
        </button>
      </div>
    </form>
    <div class="card mt-2">
      <div class="card-body p-2">
        {{ todos[0].subject}}
      </div>
    </div>
    <div class="card mt-2">
      <div class="card-body p-2">
        {{ todos[1].subject}}
      </div>
    </div>
  </div>
</template>

<!-- javascript 로직이 들어감 -->
<script>
  import { ref } from 'vue';

  export default {
    setup() {
      const todo = ref('');
      const todos = ref([
        {id:1, subject: '휴대폰 사기'},
        {id:2, subject: '장보기'},
      ]);

      const onSubmit = () => {
        todos.value.push({
          id: Date.now(),
          subject: todo.value
        });
      };

      return {
        todo,
        todos,
        onSubmit,
      }

    }
  }
</script>
<!-- css 코드가 들어감 -->
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
