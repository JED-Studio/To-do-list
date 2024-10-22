<script>
import { defineComponent, ref } from 'vue'

import AppTodoItem from './AppTodoItem.vue'

export default defineComponent({
  components: {
    AppTodoItem
  },

  props: {
    items: {
      type: Array,
      id: Number,
      completed: Boolean,
      required: true
    }
  },

  setup(props, { emit }) {
    const toggle = (id) => {
      emit('toggleItem', id)
    }

    const remove = (id) => {
      emit('removeItem', id)
    }

    return {
      toggle,
      remove
    }
  }
})
</script>

<template>
  <ul class="todo-list">
    <AppTodoItem
      v-for="item in items"
      :key="item.id"
      :id="item.id"
      :text="item.text"
      :completed="item.completed"
      @toggle="toggle"
      @remove="remove"
    />
  </ul>
</template>
