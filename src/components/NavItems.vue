<template>
  <nav class="navbar bg-body-tertiary">
    <div class="container-fluid">
      <h1 class="navbar-brand">Todos</h1>
      <form class="d-flex" role="search" @submit.prevent="createTodo">
        <input
          class="form-control me-2"
          type="search"
          placeholder="TODO를 입력하세요."
          aria-label="TODO를 입력하세요."
          :value="todoText"
          @input="(event) => $emit('update:todoText', event.target.value)"
        />
        <button class="btn btn-outline-success" type="submit">SAVE</button>
      </form>
    </div>
  </nav>
</template>

<script>
export default {
  props: ['todoText'],
  emit: ['submit', 'update:todoText'],
  setup() {
    return {}
  }
}
</script>

<style lang="scss" scoped></style>
