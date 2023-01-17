<script setup lang="ts">
import { ref } from "vue";
import TodoItem from "./TodoItem.vue";
import type { Item } from "../types/item";

const newItemLabel = ref("");
const list = ref<Item[]>([{ id: 1, label: "Add Slots", isComplete: false }]);

const generateId = () => {
  return Math.max(0, ...list.value.map((item) => item.id)) + 1;
};

const addItem = (event: Event) => {
  event.preventDefault();

  list.value.push({
    id: generateId(),
    label: newItemLabel.value,
    isComplete: false,
  });
  newItemLabel.value = "";
};

const toggleItemComplete = (id: number) => {
  const item = list.value.find((item) => item.id === id);
  if (item) {
    item.isComplete = !item.isComplete;
  }
};

const deleteItem = (id: number) => {
  list.value = list.value.filter((item) => item.id !== id);
};
</script>

<template>
  <div class="wrapper">
    <form @submit="addItem">
      <input v-model="newItemLabel" autofocus placeholder="Add New Item" />
      <input type="submit" value="Add" />
    </form>
    <ul>
      <li v-for="item in list" :key="item.id">
        <slot
          :item="item"
          :completeItem="toggleItemComplete"
          :deleteItem="deleteItem"
        >
          <TodoItem
            :item="item"
            @complete="toggleItemComplete"
            @delete="deleteItem"
          />
        </slot>
      </li>
    </ul>
  </div>
</template>

<style lang="scss">
.wrapper {
  margin: 2rem;
}

ul {
  list-style: none;
  margin: 1rem 0;
  padding: 0;

  li p {
    display: inline-block;
    margin: 0 1rem;
    font-size: 1.25rem;
  }
}

.complete {
  text-decoration: line-through;
}
</style>
