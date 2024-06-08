<template>
  <div class="container mx-auto min-h-screen flex flex-col">
    <header class="flex justify-between items-center py-4">
      <h1 class="text-2xl font-bold">My Notes</h1>
      <input
        type="text"
        placeholder="Search"
        class="border rounded px-4 py-2"
      />
    </header>
    <SliderBanner />
    <div
      class="flex-grow grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4 p-4"
    >
      <Note v-for="note in notes" :key="note.id" :note="note" />
    </div>
    <footer
      class="text-center py-4 fixed bottom-0 left-0 w-full bg-white border-t"
    >
      <p>Footer - Didin Nur Yahya - 08/06/2024</p>
    </footer>
  </div>
</template>

<script setup>
import { ref } from "vue";
import SliderBanner from "~/components/SliderBanner.vue";
import Note from "~/components/Note.vue";

const notes = ref(
  Array.from({ length: 20 }, (v, i) => ({
    id: i + 1,
    title: `Notes title ${i + 1}`,
    content: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. ...",
  }))
);
</script>
