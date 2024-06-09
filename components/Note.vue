<template>
  <div
    class="bg-white border rounded-lg shadow p-4 h-[200px] overflow-hidden cursor-pointer relative"
  >
    <h2 class="font-bold mb-2" @click="handleClick">{{ note.title }}</h2>
    <p class="text-sm" @click="handleClick">{{ note.description }}</p>
    <button
      class="absolute top-2 right-2 bg-white-500 text-white rounded-full p-2"
      @click.stop="handleDelete"
    >
      🗑️
    </button>
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from "vue";

const props = defineProps({
  note: {
    type: Object,
    required: true,
  },
});

const emit = defineEmits(["click", "delete"]);

const handleClick = () => {
  emit("click", props.note);
};

const handleDelete = () => {
  emit("delete", props.note);
};
</script>
