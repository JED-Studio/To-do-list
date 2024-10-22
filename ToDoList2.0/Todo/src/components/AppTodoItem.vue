<script>
import { defineComponent, ref } from 'vue'

export default defineComponent({
  props: {
    id: Number,
    text: String,
    item: Object,
    completed: Boolean
  },



  setup(props, { emit }) {
    const toggle = () => {
      emit('toggle', props.id)
    }
    const remove = () => {
      emit('remove', props.id)
    }

    return {
      toggle,
      remove
    }
  }
})
</script>

<template>
  <li class="todo-item" :class="{ 'todo-item--done': completed }" @click="toggle">
    <div class="todo-item__status">
      <i class="bi bi-check2"></i>
    </div>
    <span class="todo-item__text">{{ text }}</span>
    <button class="todo-item__remove-button" @click.stop="remove">
      <i class="bi bi-trash3"></i>
    </button>
  </li>
</template>
