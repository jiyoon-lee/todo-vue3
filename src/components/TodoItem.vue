<template>
  <div class="form-check d-flex gap-2">
    <input
      class="form-check-input"
      type="checkbox"
      id="flexCheckDefault"
      :value="item.active"
      @change="$emit('changeActive', item.id)"
      v-show="!item.editMode"
    />
    <input
      type="text"
      class="form-control"
      v-if="item.editMode"
      :value="modelValue"
      @input="$emit('update:modelValue', item.id, $event.target.value)"
      @blur="$emit('doneEdit', item.id)"
      @keyup.enter="$emit('doneEdit', item.id)"
      @keyup.esc="$emit('changeEditMode', item.id)"
    />
    <span
      v-else
      class="form-check-label"
      for="flexCheckDefault"
      :style="item.active || 'text-decoration: line-through'"
      @dblclick="$emit('changeEditMode', item.id)"
    >
      {{ item.text }}
    </span>
    <button
      type="button"
      class="btn btn-secondary"
      style="--bs-btn-padding-y: 0.25rem; --bs-btn-padding-x: 0.5rem; --bs-btn-font-size: 0.5rem"
      v-show="!item.editMode"
      @click="$emit('deleteTodo', item.id)"
    >
      ✘
    </button>
  </div>
</template>

<script>
export default {
  props: {
    item: {
      type: Object,
      required: true,
      default: () => ({})
    },
    modelValue: {
      type: String,
      required: false,
      default: ''
    }
  },
  emits: ['update:modelValue'],
  setup() {
    return {}
  }
}
</script>

<style lang="scss" scoped></style>
