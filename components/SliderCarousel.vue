<template>
  <div class="slider-container">
    <div
      class="slides"
      :style="{ transform: `translateX(${translateValue}px)` }"
    >
      <div v-for="(slide, index) in slides" :key="index" class="slide">
        <img
          :src="slide.image"
          :alt="'Slide ' + (index + 1)"
          class="slide-image"
        />
      </div>
    </div>
    <button class="prev" @click="scroll('left')">Prev</button>
    <button class="next" @click="scroll('right')">Next</button>
  </div>
</template>

<script setup>
import { ref } from "vue";

const slides = ref([
  { image: "https://via.placeholder.com/800x200?text=Slide+1" },
  { image: "https://via.placeholder.com/800x200?text=Slide+2" },
  { image: "https://via.placeholder.com/800x200?text=Slide+3" },
]);
const translateValue = ref(0);
const slideWidth = 100; // Width of each slide in percentage

const scroll = (direction) => {
  const containerWidth = document.querySelector(".slider-container").offsetWidth;
  const totalWidth = slides.value.length * slideWidth;
  
  if (direction === 'left' && translateValue.value < 0) {
    translateValue.value += slideWidth;
  } else if (direction === 'right' && translateValue.value > -(totalWidth - containerWidth)) {
    translateValue.value -= slideWidth;
  }
};
</script>

<style scoped>
.slider-container {
  position: relative;
  overflow: hidden;
}
.slides {
  display: flex;
  transition: transform 0.5s ease;
}
.slide {
  flex: 0 0 auto;
  width: 100%;
}
.slide-image {
  width: 100%;
  height: auto;
}
.prev,
.next {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  padding: 8px 16px;
  border: none;
  border-radius: 4px;
  background-color: #000;
  color: #fff;
  cursor: pointer;
}
.prev {
  left: 0;
}
.next {
  right: 0;
}
</style>
