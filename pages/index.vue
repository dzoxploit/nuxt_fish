<template>
  <div class="container mx-auto min-h-screen flex flex-col">
    <header class="flex justify-between items-center py-4">
      <h1 class="text-2xl font-bold">My Notes</h1>
      <input
        type="text"
        placeholder="Search"
        class="border rounded px-4 py-2"
        v-model="searchQuery"
        @input="fetchNotes"
      />
    </header>
    <div
      class="flex-grow grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4 p-4"
    >
      <Note
        v-for="note in notes"
        :key="note.id"
        :note="note"
        @click="openModal(note)"
        @delete="deleteNote"
      />
    </div>
    <footer
      class="text-center py-4 fixed bottom-0 left-0 w-full bg-white border-t"
    >
      <p>Footer - Didin Nur Yahya - 08/06/2024</p>
    </footer>
    <NoteModal
      v-if="isModalOpen"
      :note="selectedNote"
      :isOpen="isModalOpen"
      @close="closeModal"
      @update="handleUpdate"
    />
  </div>
</template>

<script setup>
import { ref, watch, onMounted } from "vue";
import axios from "axios";
import Note from "~/components/Note.vue";
import NoteModal from "~/components/NoteModal.vue";

const notes = ref([]);
const searchQuery = ref("");
const isModalOpen = ref(false);
const selectedNote = ref(null);

const fetchNotes = async () => {
  try {
    const response = await axios.get(
      `http://localhost:8000/api/messages?search=${searchQuery.value}`
    );
    notes.value = response.data.data;
  } catch (error) {
    console.error("Error fetching notes:", error);
  }
};

watch(searchQuery, fetchNotes);

onMounted(() => {
  fetchNotes();
});

const openModal = (note) => {
  selectedNote.value = note;
  isModalOpen.value = true;
};

const closeModal = () => {
  isModalOpen.value = false;
};

const handleUpdate = async (updatedNote) => {
  const index = notes.value.findIndex((note) => note.id === updatedNote.id);
  if (index !== -1) {
    notes.value[index] = updatedNote;
  }
  await fetchNotes(); // Refresh the data
  closeModal(); // Close the modal
  await fetchNotes();
};

const deleteNote = async (note) => {
  try {
    await axios.delete(`http://localhost:8000/api/messages/${note.id}`);
    await fetchNotes(); // Refresh the data after deletion
  } catch (error) {
    console.error("Error deleting note:", error);
  }
};
</script>
