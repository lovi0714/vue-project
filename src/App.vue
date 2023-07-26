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
    <!-- 자식 컴포넌트에서 설정한 이벤트 이름을 사용 -->
    <TodoSimpleForm @add-todo="addTodo" />

    <div v-if="!todos.length">
      추가된 Todo가 없습니다.
    </div>
    <!-- :props로 보낼 이름 = "데이터"-->
    <TodoList 
      :todos="todos" 
      @toggle-todo="toggleTodo"
      @delete-todo="deleteTodo"
    />
    
  </div>
</template>

<!-- javascript 로직이 들어감 -->
<script>
  import { ref } from 'vue';
  import TodoSimpleForm from './components/TodoSimpleForm.vue';
  import TodoList from './components/TodoList.vue';

  export default {
    components : {
      TodoSimpleForm,
      TodoList,
    },
    setup() {
      //const toggle = ref(false);

      const todos = ref([]);
      /*
      const todoStyle = {
        textDecoration: 'line-through',
        color: 'gray'
      }
      */

      const addTodo = (todo) => {
        console.log(todo);
        todos.value.push(todo);
      }

      const toggleTodo = (index) => {
        todos.value[index].completed = !todos.value[index].completed;
      }
    
      /*
      const onToggle = () => {
        toggle.value = !toggle.value;
      }
      */
      const deleteTodo = (index) => {
          todos.value.splice(index, 1);
      }


      return {
        todos,
        deleteTodo,
        addTodo,
        toggleTodo,
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
