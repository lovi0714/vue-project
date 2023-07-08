<template>
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
</template>

<script>
export default {
    //props: ['todos']
    props: {
        todos: {
            type: Array,
            required: true
        }
    }
}
</script>

<style>

</style>