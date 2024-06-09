<template>
  <div
    class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50 z-50"
    v-if="isOpen"
  >
    <div class="bg-white rounded-lg p-8 w-full max-w-md">
      <h2 class="text-2xl font-bold mb-4">Edit Note</h2>
      <label class="block mb-2">
        Title:
        <input
          type="text"
          class="border rounded px-4 py-2 w-full"
          v-model="updatedNote.title"
        />
      </label>
      <label class="block mb-2">
        Description:
        <textarea
          class="border rounded px-4 py-2 w-full"
          v-model="updatedNote.description"
        ></textarea>
      </label>
      <div class="flex justify-end space-x-4 mt-4">
        <button class="bg-gray-300 px-4 py-2 rounded" @click="closeModal">
          Cancel
        </button>
        <button
          class="bg-blue-500 text-white px-4 py-2 rounded"
          @click="updateNote"
        >
          Save
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, watch } from "vue";
import axios from "axios";

const props = defineProps({
  note: {
    type: Object,
    required: true,
  },
  isOpen: {
    type: Boolean,
    required: true,
  },
});

const emit = defineEmits(["close", "update", "fetchNotes"]);

const updatedNote = ref({ ...props.note });

watch(
  () => props.note,
  (newNote) => {
    updatedNote.value = { ...newNote };
  }
);

const closeModal = () => {
  emit("close");
  emit("fetchNotes"); // Emit event to fetch notes when modal is closed
};

const updateNote = async () => {
  try {
    const response = await axios.put(
      `http://localhost:8000/api/messages/${props.note.id}`,
      {
        title: updatedNote.value.title,
        description: updatedNote.value.description,
      }
    );
    emit("update", response.data.data);
    emit("fetchNotes"); // Emit event to fetch notes after updating
    closeModal();
  } catch (error) {
    console.error("Error updating note:", error);
  }
};
</script>

<style scoped>
/* Add any specific styling for your modal here */
</style>
