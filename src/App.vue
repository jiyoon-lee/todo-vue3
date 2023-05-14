<template>
  <div>
    <h1>Todos</h1>
    <form action="" @submit.prevent="submit">
      <input type="text" v-model.trim="todo" />
      <input type="submit" value="SAVE" />
    </form>
    <ul>
      <li v-for="item in getTodos" :key="item.id">
        <input
          type="text"
          v-if="item.editMode"
          @blur="doneEdit(item.id, $event)"
          @keyup.enter="doneEdit(item.id, $event)"
          @keyup.esc="item.editMode = false"
        />
        <div v-else>
          <input type="checkbox" id="checkbox" v-model="item.active" />
          <span
            :style="item.active || 'text-decoration: line-through'"
            @dblclick="item.editMode = true"
            >{{ item.text }}</span
          >
          <button @click="deleteTodo(item.id)">✘</button>
        </div>
      </li>
    </ul>
    <div class="actions-container">
      <div>{{ activeItemNum + ' items left' }}</div>
      <div>
        <button @click="filterType = 'all'">All</button>
        <button @click="filterType = 'active'">Active</button>
        <button @click="filterType = 'completed'">Completed</button>
      </div>
      <button @click="clear">Clear completed</button>
    </div>
  </div>
</template>

<script>
import { ref, reactive, computed } from 'vue'
export default {
  setup() {
    const filterType = ref('all')
    const todo = ref('')
    let todos = reactive({
      list: []
    })
    const submit = () => {
      console.log('submit')
      todos.list.push({
        id: todos.list.length,
        text: todo.value,
        active: true,
        editMode: false
      })
      todo.value = ''
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
    const doneEdit = (id, e) => {
      todos.list = todos.list.map((element) => {
        if (element.id === id) {
          return {
            ...element,
            text: e.target.value,
            editMode: false
          }
        } else return element
      })
    }
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
    return {
      todo,
      getTodos,
      filterType,
      activeItemNum,
      submit,
      doneEdit,
      deleteTodo,
      clear
    }
  }
}
</script>

<style scoped>
.actions-container {
  display: flex;
  column-gap: 30px;
}
</style>
