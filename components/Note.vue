<template>
  <div class="bg-white border rounded-lg shadow p-4 h-[200px] overflow-hidden">
    <h2 class="font-bold mb-2">{{ note.title }}</h2>
    <p class="text-sm">{{ note.content }}</p>
  </div>
</template>

<script setup>
import { defineProps } from "vue";

const props = defineProps({
  note: {
    type: Object,
    required: true,
  },
});
</script>
