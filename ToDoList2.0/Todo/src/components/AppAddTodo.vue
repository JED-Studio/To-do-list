<script>
import { defineComponent, ref } from 'vue'

export default defineComponent({
  setup(props, { emit }) {
    const Form = ref(false)
    const todoText = ref('')

    const showForm = () => {
      Form.value = false
    }

    const closeForm = () => {
      Form.value = true
    }

    const addTodo = () => {
      emit('addTodo', {
        id: Date.now(),
        text: todoText.value,
        completed: false
      })

      todoText.value = ''
    }

    return {
      addTodo,
      todoText,
      Form,
      showForm,
      closeForm
    }
  }
})
</script>

<template>
  <section class="add-todo">
    <form v-if="Form" @submit.prevent="addTodo" class="add-todo__form">
      <button class="close-button" type="button" @click="showForm">
        <i class="bi bi-x"></i>
      </button>
      <div class="text-input text-input--focus">
        <input class="input" v-model="todoText" />
      </div>
      <button class="button button--filled">Add task</button>
    </form>
    <button v-else class="add-todo__show-form-button" @click="closeForm">
      <i class="bi bi-plus-lg"></i>
    </button>
  </section>
</template>
