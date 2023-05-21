<template>
  <div class="container">
    <NaviItems v-model:todoText="todo" @submit="createTodo" />
    <div class="card text-center">
      <TodoItems
        v-if="getTodos.length > 0"
        :items="getTodos"
        @doneEdit="doneEdit"
        @changeTodoText="changeTodoText"
        @changeEditMode="changeEditMode"
        @changeActive="changeActive"
        @deleteTodo="deleteTodo"
      />
      <div v-else class="my-4">등록된 정보가 없습니다.</div>
      <TodosAction
        :activeItemNum="activeItemNum"
        :filterType="filterType"
        @clear="clear"
        @changeFilterType="changeFilterType"
      />
    </div>
  </div>
</template>

<script>
import NaviItems from '@/components/NavItems.vue'
import TodoItems from '@/components/TodoItems.vue'
import TodosAction from '@/components/TodosAction.vue'
import { ref, reactive, computed } from 'vue'
export default {
  components: {
    NaviItems,
    TodoItems,
    TodosAction
  },
  setup() {
    const filterType = ref('all')
    const todo = ref('')
    let todos = reactive({
      list: []
    })
    const createTodo = () => {
      if (todo.value) {
        todos.list.push({
          id: todos.list.length,
          text: todo.value,
          active: true,
          editMode: false
        })
        todo.value = ''
      }
    }
    const getTodos = computed(() => {
      if (filterType.value === 'all') {
        return todos.list
      } else if (filterType.value === 'active') {
        return todos.list.filter((item) => item.active)
      } else {
        return todos.list.filter((item) => !item.active)
      }
    })
    // 남은 활성화 todo 개수
    const activeItemNum = computed(() => todos.list.filter((item) => item.active).length)
    // todo 제거
    const deleteTodo = (id) => {
      todos.list = todos.list.filter((item) => item.id !== id)
    }
    // 전체 지우기
    const clear = () => {
      todos.list = []
    }
    const doneEdit = (id) => {
      todos.list = todos.list.map((element) => {
        if (element.id === id) {
          return {
            ...element,
            editMode: false
          }
        } else return element
      })
    }
    const changeFilterType = (value) => (filterType.value = value)
    const changeTodoText = (id, text) => {
      todos.list = todos.list.map((element) => {
        if (element.id === id) {
          return {
            ...element,
            text
          }
        } else return element
      })
    }
    const changeEditMode = (id) => {
      todos.list = todos.list.map((item) => {
        if (item.id === id) {
          return {
            ...item,
            editMode: !item.editMode
          }
        } else return item
      })
    }
    const changeActive = (id) => {
      todos.list = todos.list.map((item) => {
        if (item.id === id) {
          return {
            ...item,
            active: !item.active
          }
        } else return item
      })
    }
    return {
      todo,
      getTodos,
      filterType,
      activeItemNum,
      createTodo,
      doneEdit,
      deleteTodo,
      clear,
      changeTodoText,
      changeFilterType,
      changeEditMode,
      changeActive
    }
  }
}
</script>

<style scoped>
.container {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 60%;
}
</style>
