<template>
  <div class="card-header">
    <div class="d-flex align-items-center gap-3 mb-2">
      <div>{{ activeItemNum + ' items left' }}</div>
      <button type="button" class="btn btn-outline-primary" @click="$emit('clear')">
        Clear completed
      </button>
    </div>
    <ul class="nav nav-pills card-header-pills justify-content-end">
      <li class="nav-item">
        <button
          class="nav-link"
          :class="filterType === 'all' && 'active'"
          @click="$emit('changeFilterType', 'all')"
        >
          All
        </button>
      </li>
      <li class="nav-item">
        <button
          class="nav-link"
          :class="filterType === 'active' && 'active'"
          @click="$emit('changeFilterType', 'active')"
        >
          Active
        </button>
      </li>
      <li class="nav-item">
        <button
          class="nav-link"
          :class="filterType === 'completed' && 'active'"
          @click="$emit('changeFilterType', 'completed')"
        >
          Completed
        </button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    filterType: {
      type: String,
      required: false,
      default: 'all'
    },
    activeItemNum: {
      type: Number,
      required: false,
      default: 0
    }
  },
  setup() {
    return {}
  }
}
</script>

<style lang="scss" scoped></style>
