<template>
  <div class="card-body">
    <ul class="list-group list-group-flush">
      <li v-for="item in items" :key="item.id" class="list-group-item">
        <TodoItem
          :item="item"
          :modelValue="item.text"
          @doneEdit="(id) => $emit('doneEdit', id)"
          @update:modelValue="(id, text) => $emit('changeTodoText', id, text)"
          @changeActive="(id) => $emit('changeActive', id)"
          @changeEditMode="(id) => $emit('changeEditMode', id)"
          @deleteTodo="(id) => $emit('deleteTodo', id)"
        />
      </li>
    </ul>
  </div>
</template>

<script>
import TodoItem from '@/components/TodoItem.vue'
export default {
  components: {
    TodoItem
  },
  props: {
    items: {
      type: Array,
      required: false,
      default: () => []
    }
  },
  setup() {}
}
</script>

<style lang="scss" scoped></style>
