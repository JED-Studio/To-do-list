<script lang="ts">
import { defineComponent, ref, computed } from 'vue'

import AppHeader from './components/AppHeader.vue'
import AppFilters from './components/AppFilters.vue'
import AppAddTodo from './components/AppAddTodo.vue'
import AppTodoList from './components/AppTodoList.vue'
import AppFooter from './components/AppFooter.vue'
import AppSwitch from './components/AppSwitch.vue'

export default defineComponent({
  components: {
    AppSwitch,
    AppHeader,
    AppFilters,
    AppAddTodo,
    AppTodoList,
    AppFooter
  },


  setup() {
    const items = ref([])
    const filter = ref('all')


    const filteredItems = computed(() => {
      if (filter.value === 'active') {
        return items.value.filter(item => !item.completed);
      } else if (filter.value === 'done') {
        return items.value.filter(item => item.completed);
      }
      return items.value; 
    });   

    const updateFilter = (newFilter: string) => {
    filter.value = newFilter
  }


    const addTodo = (newTodo) => {
      items.value.push(newTodo)
    }

    const toggleItem = (id) => {
      const item = items.value.find((item) => item.id === id)
      if (item) {
        item.completed = !item.completed
      }
    }

    const removeItem = (id) => {
      items.value = items.value.filter((item) => item.id !== id);
    };

    return {
      items, // Make the todos array available to the AppTodoList component
      addTodo,
      removeItem,
      toggleItem,
      filteredItems,
      updateFilter
    }
  }
})
</script>

<template>
<div class="body">
  <AppSwitch />
  
  <div class="flex">
    <div class="main">
    <AppHeader />
    <AppFilters  
    v-model:filter="filter"
    @update:filter="updateFilter"
    />
    <AppTodoList  :items="filteredItems" @removeItem="removeItem" @toggleItem="toggleItem"/>
    <AppAddTodo @addTodo="addTodo" />
    <AppFooter />
  </div>
</div>
</div>
</template>

<style>
:root {
  --light: #d8dbe0;
  --dark: #28292c;
  --link: rgb(27, 129, 112);
  --link-hover: rgb(24, 94, 82);
}
:root {
  --background-color-primary: #090b16;
  --background-color-secondary:#090b16;
  --background-color-luna:#ffffff ;
  --background-color-ul:rgba(255, 255, 255, .05);
  --accent-color: #cacaca;
  --text-primary-color:  white;
  --text-color:white;
  --text-color-h1:rgb(255, 255, 255);
  --text-color-h2:rgba(255, 255, 255, .5);
  --element-size: 4rem;
  transition: 0.5s;
  
}

/* Define styles for the root window with dark - mode preference */
:root.dark-theme {
  --background-color-primary: #ffffff;
  --background-color-secondary: #2d2d30;
  --background-color-luna:#000000 ;
  --background-color-ul:rgb(0, 0, 0);
  --accent-color: #3f3f3f;
  --text-primary-color: #ddd;
  --text-color:rgb(255, 255, 255);
  --text-color-h1:rgb(0, 0, 0);
  --text-color-h2:rgba(0, 0, 0, 0.5);

}


.alva{
  background-color: var(--background-color-primary);
  transition: 0.5s;
}
</style>