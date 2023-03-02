<script setup>
  import { ref, onMounted, computed, watch } from 'vue'

  const items = ref([])
  const name = ref('')

  const input_content = ref('')
  const input_category = ref(null)

  const items_asc = computed(() => todos.value.sort((a, b) => {
    return b.createdAt - a.createdAt
  }))

  const addItem = () => {}

  watch(name, (newVal) => {
    localStorage.setItem('name', newVal)
  })

  onMounted(() => {
    name.value = localStorage.getItem('name') || ''
  })
</script>

<template>
  <main class="app">
    <section class="greeting">
      <h2 class="title">
        Hello, <input type="text" placeholder="_" v-model="name">
      </h2>
    </section>

    <section class="create-todo">
      <h3>PROGRESS</h3>

      <form @submit.prevent="addTodo">
        <h4>What's on your list?</h4>
        <input type="text" placeholder="e.g. make a video" v-model="input_content">

        <h4>Pick a category</h4>

        <div class="options">
          <label>
            <input 
              type="radio"
              name="category"
              value="business"
              v-model="input_category"
            >
            <span class="bubble business"></span>
            <div>Business</div>
          </label>

          <label>
            <input 
              type="radio"
              name="category"
              value="personal"
              v-model="input_category"
            >
            <span class="bubble personal"></span>
            <div>Personal</div>
          </label>
        </div>

        <input type="submit" value="Add Item">
      </form>
    </section>
  </main>
</template>
