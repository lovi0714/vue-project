<template>
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

</template>

<script>
    import { ref } from 'vue';

    export default {
        emits: ['add-todo'],
        setup(props, { emit }) {
            const todo = ref('');
            const hasError = ref(false);

            const onSubmit = () => {
                if (todo.value === ''){
                    hasError.value = true;
                } else {
                  // todos 배열이 App.vue에 있어서 사용할 수 없음.
                  // 자식 컴포넌트에서 데이터를 부모 컴포넌트로 올리려면, emit을 사용해준다.
                  // props, context(자식 -> 부모로 데이터 보낼 때 필요함)를 받아와서 사용
                  // emit('이벤트 이름', {주고싶은 데이터 이름: 데이터})
                  
                    emit('add-todo', {
                        id: Date.now(),
                        subject: todo.value,
                        completed: false,
                    });
                //     todos.value.push({
                //     id: Date.now(),
                //     subject: todo.value,
                //     completed: false,
                // });
                    hasError.value = false;
                    todo.value = '';
                }
            };
            
            return{
                todo,
                hasError,
                onSubmit,
            }
        }
    }
</script>

<style>

</style>