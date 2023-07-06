<!-- .vue 파일은 3가지로 이루어져 있음 --> 

<!-- html 코드가 들어감 -->
<template>
<!-- 
  v-show 사용, 초기 렌더링 비용이 높음, 토글 비용이 낮음 (토글이 잦은 기능에 적용하면 좋음)
  <div v-show="toggle">true</div>
  <div v-show="!toggle">false</div>

  v-if는 렌더링 할 때부터 조건에 맞는 태그만 가져옴, 토글하는데 비용이 많이 든다. (런타임 동안에 거의 안 바뀔 기능에 적용하는 것이 좋음) 
  <div v-if="toggle">true</div>
  <div v-else>false</div>
  <button @click="onToggle">Toggle</button>
-->
  <div class="container">
    <h2>To-Do List</h2>
    <form @submit.prevent="onSubmit">
      <div class="d-flex">
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
      </div>
      <div v-show="hasError" style="color: red">
        This field cannot be empty
      </div>
    </form>
    <div v-if="!todos.length">
      추가된 Todo가 없습니다.
    </div>
    
    <!-- v-for를 사용할 때는 키를 넣어주어야함 (key 바인딩 필요) -->
    <div 
      v-for="(todo, index) in todos"
      :key="todo.id"
      class="card mt-2"
    >
      <div class="card-body p-2 d-flex align-items-center">
        <div class="form-check flex-grow-1">
          <input class="form-check-input" type="checkbox" v-model="todo.completed">
          <!-- 
            style 바인딩 방식 
          <label class="form-check-label" :style="todo.completed ? todoStyle : {}">{{ todo.subject}}</label>
          -->
          <!-- class 바인딩 방식 -->
          <label class="form-check-label" :class="{ todo: todo.completed}">{{ todo.subject}}</label>
        </div>
        <div>
          <button class="btn btn-danger btn-sm" @click="deleteTodo(index)">Delete</button>
        </div>
      </div>
    </div>
  </div>
</template>

<!-- javascript 로직이 들어감 -->
<script>
  import { ref } from 'vue';

  export default {
    setup() {
      const toggle = ref(false);
      const todo = ref('');
      const todos = ref([]);

      const hasError = ref(false);
      const todoStyle = {
        textDecoration: 'line-through',
        color: 'gray'
      }

      const onSubmit = () => {
        if (todo.value === ''){
          hasError.value = true;
        } else {
        todos.value.push({
          id: Date.now(),
          subject: todo.value,
          completed: false,
        });
        hasError.value = false;
        todo.value = '';
        }
      };

      const onToggle = () => {
        toggle.value = !toggle.value;
      }

      const deleteTodo = (index) => {
          todos.value.splice(index, 1);
      }

      return {
        todo,
        todos,
        toggle,
        hasError,
        todoStyle,
        deleteTodo,
        onToggle,
        onSubmit,
      }

    }
  }
</script>
<!-- css 코드가 들어감 -->
<style>
 .todo {
  color: gray;
  text-decoration: line-through;
 }
</style>
