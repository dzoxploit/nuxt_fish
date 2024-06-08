<template>
  <div
    class="flex justify-between items-center bg-gray-300 p-4 my-4 h-[300px] rounded-lg overflow-hidden"
  >
    <button class="text-2xl" @click="prevSlide">&lt;</button>
    <div class="flex-1 text-center">
      <!-- Tampilkan gambar saat ini -->
      <img :src="currentImage" alt="Slider Image" />
    </div>
    <button class="text-2xl" @click="nextSlide">&gt;</button>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

// Daftar gambar dummy
const images = [
  "https://via.placeholder.com/300x150",
  "https://via.placeholder.com/300x150",
  "https://via.placeholder.com/300x150",
  // Tambahkan lebih banyak URL gambar dummy di sini
];

// State untuk menyimpan indeks gambar saat ini
const currentImageIndex = ref(0);

// Ambil URL gambar saat ini berdasarkan indeks
const currentImage = computed(() => images[currentImageIndex.value]);

// Logika untuk mengubah ke gambar sebelumnya
const prevSlide = () => {
  currentImageIndex.value =
    (currentImageIndex.value - 1 + images.length) % images.length;
};

// Logika untuk mengubah ke gambar berikutnya
const nextSlide = () => {
  currentImageIndex.value = (currentImageIndex.value + 1) % images.length;
};
</script>

<style scoped>
/* Additional styles if needed */
</style>
