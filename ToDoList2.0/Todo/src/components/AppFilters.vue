<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({

  props: {
    filter:{
      type: String,
      required: true
    }
  },

  setup(props,{emit}) {
    const setFilter = (addfilter: string) => {
      emit('update:filter',addfilter)
    }

    return {
      setFilter
    }
  }
})
</script>


<template>
  <aside class="app-filters">
    <section class="toggle-group">
      <button class="button" :class="{ 'button--primary': filter === 'all' }" @click="setFilter('all')">All</button>
      <button class="button" :class="{ 'button--primary': filter === 'active' }" @click="setFilter('active')">Active</button>
      <button class="button" :class="{ 'button--primary': filter === 'done' }" @click="setFilter('done')">Done</button>
    </section>
  </aside>
</template>
