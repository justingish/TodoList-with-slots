<script setup lang="ts">
import TodoList from "./components/TodoList.vue";
</script>

<template>
  <main>
    <section>
      <h1>TodoList with Default Content</h1>
      <TodoList />
    </section>

    <section>
      <h1>TodoList with Custom Slot</h1>
      <TodoList #="{ item, completeItem }">
        <div @click="completeItem(item.id)" class="custom-list">
          <span>{{ item.label }}</span>
          <span v-if="item.isComplete">&#9989;</span>
          <span v-else>&#11093;</span>
        </div>
      </TodoList>
    </section>
  </main>
</template>

<style>
section {
  margin-top: 100px;
}
.custom-list span {
  display: inline-block;
  margin: 0 1rem;
}
</style>
