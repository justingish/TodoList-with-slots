<script setup lang="ts">
import type { Item } from "../types/item";

interface Props {
  item: Item;
}

const props = defineProps<Props>();
const emit = defineEmits<{
  (e: "complete", id: number): void;
  (e: "delete", id: number): void;
}>();
</script>

<template>
  <label>
    <input
      type="checkbox"
      :value="props.item.isComplete"
      @change="emit('complete', props.item.id)"
    />
    <p :class="props.item.isComplete ? 'complete' : ''">
      {{ props.item.label }}
    </p>
  </label>
  <span @click="emit('delete', props.item.id)">X</span>
</template>
