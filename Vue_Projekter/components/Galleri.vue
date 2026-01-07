<script setup>
import { ref, computed } from 'vue'

import BowlingImg from '../assets/img/Bowling.webp'
import GokartImg from '../assets/img/Gokart.webp'
import LasergameImg from '../assets/img/Lasergame.webp'
import LegelandImg from '../assets/img/Legeland.webp'
import SpillehalImg from '../assets/img/Spillehal.webp'
import VirtualrealityImg from '../assets/img/VirtualReality.webp'
import VREscapeImg from '../assets/img/VREscape.webp'

const baseCards = [
  { image: BowlingImg },
  { image: GokartImg },
  { image: LasergameImg },
  { image: LegelandImg },
  { image: SpillehalImg },
  { image: VirtualrealityImg },
  { image: VREscapeImg }
]

const cardsPerPage = 3
const activePage = ref(0)

const cards = computed(() => {
  const result = [...baseCards]
  while (result.length < cardsPerPage * Math.ceil(baseCards.length / cardsPerPage) + cardsPerPage) {
    result.push(...baseCards)
  }
  return result
})

const pages = computed(() =>
  Math.ceil(baseCards.length / cardsPerPage)
)

const translateX = computed(() => {
  const cardWidth = 300
  const gap = 32
  const pageWidth = (cardWidth + gap) * cardsPerPage
  return `translateX(-${activePage.value * pageWidth}px)`
})

const goToPage = (page) => {
  if (page < 0) {
    activePage.value = pages.value - 1
  } else if (page >= pages.value) {
    activePage.value = 0
  } else {
    activePage.value = page
  }
}
</script>

<template>
  <section class="gallery">
    <div class="viewport">
      <div class="track" :style="{ transform: translateX }">
        <div
          v-for="(card, index) in cards"
          :key="index"
          class="gallery-card"
        >
          <img :src="card.image" alt="" />
        </div>
      </div>
    </div>

    <div class="dots">
      <span
        v-for="i in pages"
        :key="i"
        :class="{ active: i - 1 === activePage }"
        @click="goToPage(i - 1)"
      />
    </div>
  </section>
</template>

<style scoped>
.gallery {
  width: 100%;
  margin: 0 auto 6rem;
}

.viewport {
  overflow: hidden;
}

.track {
  display: flex;
  gap: 2rem;
  transition: transform 0.5s ease;
}

.gallery-card {
  flex: 0 0 300px;
  height: 420px;
}

.gallery-card img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.dots {
  display: flex;
  justify-content: center;
  margin-top: 1rem;
  gap: 0.5rem;
}

.dots span {
  width: 14px;
  height: 14px;
  border-radius: 50%;
  background: #154B82;
  cursor: pointer;
}

.dots span.active {
  background: #D41E2A;
}

@media (max-width: 400px) {
  .viewport {
    overflow-x: auto;
  }
  .track {
    gap: 1rem;
    transform: none !important;
  }
  .gallery-card {
    flex: 0 0 200px;
    height: 280px;
  }
  .gallery-card img {
    object-fit: cover;
  }
}
</style>
