<script setup>
import { ref } from 'vue'

import Header from '../components/navigation.vue'
import Footer from '../components/Footer.vue'

import BowlingImg from '../assets/img/Bowling.webp'
import GokartImg from '../assets/img/Gokart.webp'
import LasergameImg from '../assets/img/Lasergame.webp'
import Legeland from '../assets/img/Legeland.webp'
import Spillehal from '../assets/img/Spillehal.webp'
import Virtualreality from '../assets/img/VirtualReality.webp'
import VREscape from '../assets/img/VREscape.webp'

const cards = [
  { title: 'Bowling', caption: 'Sjov for alle', description: 'Tag venner og familie med til bowling i moderne baner.', image: BowlingImg },
  { title: 'Gokart', caption: 'Fart og spænding', description: 'Oplev høj fart på vores indendørs gokartbane.', image: GokartImg },
  { title: 'Lasergame', caption: 'Action og taktik', description: 'Kæmp mod vennerne i vores lasergame arena.', image: LasergameImg },
  { title: 'Spillehal', caption: 'Spillehal til familien', description: 'Nyd sjove arkadespil i spillehalen.', image: Spillehal },
  { title: 'Legeland', caption: 'Legeland til børn', description: 'Sjov og leg for de mindste.', image: Legeland },
  { title: 'Virtual Reality', caption: 'Virtual reality', description: 'Oplev VR i verdensklasse.', image: Virtualreality },
  { title: 'VR Escaperoom', caption: 'Firma og grupper', description: 'Perfekt til firmaevents og grupper.', image: VREscape }
]

const openFaq = ref(null)

const faqs = [
  {
    question: 'Må man selv have mad og drikke med',
    answer: 'Nej, det er desværre ikke tilladt at medbringe egen mad og drikke. Vi har vores egen café og restaurant.'
  },
  {
    question: 'Hvornår kan vi senest afbestille arrangementet?',
    answer: 'Afbestilling skal ske senest 7 dage før arrangementets start.'
  },
  {
    question: 'Skal vi booke på forhånd?',
    answer: 'Ja, vi anbefaler altid at booke på forhånd for at sikre plads.'
  },
  {
    question: 'Hvordan foregår betaling?',
    answer: 'Betaling kan ske online ved booking eller på stedet.'
  }
]

const toggleFaq = index => {
  openFaq.value = openFaq.value === index ? null : index
}
</script>

<template>
  <Header />

  <video class="hero-video" autoplay muted loop playsinline>
    <source src="../assets/vid/BrandingVideo.mp4" type="video/mp4" />
    Your browser does not support the video tag.
  </video>

  <section>
    <h1 class="aktOverskrift">Aktiviteter</h1>
    <p class="aktParagraph">
      Hos Action House Funcenter finder du et bredt udvalg af actionfyldte og sjove aktiviteter for både børn, unge og voksne.
      Uanset om du er til fart, konkurrence eller hyggeligt samvær, har vi oplevelser, der passer til enhver anledning.
      Gå på opdagelse i vores aktiviteter herunder, og find den næste oplevelse, der sætter gang i adrenalinen og skaber minder.
    </p>
  </section>

  <section class="flip-grid">
    <div
      v-for="(card, index) in cards"
      :key="index"
      class="flip-card"
    >
      <div class="flip-card-inner">
        <div class="flip-card-front">
          <img :src="card.image" alt="" />

          <div class="front-overlay">
            <div class="text-background"></div>
            <h3>{{ card.title }}</h3>
          </div>

          <div class="flip-icon">↻</div>
        </div>

        <div class="flip-card-bagside">
          <p>{{ card.description }}</p>
        </div>
      </div>
    </div>
  </section>

  <!-- FAQ SECTION -->
  <section class="faq-section">
    <h2 class="faq-title">Ofte stillede spørgsmål</h2>

    <div
      v-for="(faq, index) in faqs"
      :key="index"
      class="faq-item"
      @click="toggleFaq(index)"
    >
      <div class="faq-header">
        <span>{{ faq.question }}</span>
        <span class="chevron" :class="{ open: openFaq === index }">⌄</span>
      </div>

      <div v-if="openFaq === index" class="faq-content">
        {{ faq.answer }}
      </div>
    </div>
  </section>

  <Footer />
</template>

<style>
.hero-video {
  width: 100%;
  height: auto;
  object-fit: cover;
}

.flip-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
  padding: var(--NormPadding);
  max-width: 1200px;
  margin: 0 auto;
}

.flip-card {
  height: 420px;
  perspective: 1000px;
}

.flip-card-inner {
  width: 100%;
  height: 100%;
  position: relative;
  transform-style: preserve-3d;
  transition: transform 0.8s;
}

.flip-card:hover .flip-card-inner {
  transform: rotateY(180deg);
}

.flip-card-front,
.flip-card-bagside {
  position: absolute;
  inset: 0;
  border-radius: 12px;
  backface-visibility: hidden;
  overflow: hidden;
}

.flip-card-front img {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.front-overlay {
  position: absolute;
  left: 0;
  bottom: 0;
  width: 100%;
  display: flex;
  align-items: center;
  padding: 0.5rem;
}

.text-background {
  position: absolute;
  left: 0;
  bottom: 0;
  width: 100%;
  height: 100px;
  background: rgba(255, 255, 255, 0.6);
  border-radius: 0 0 12px 12px;
}

.front-overlay h3 {
  margin: 0;
  font-size: 1.7rem;
  color: #154B82;
  padding-left: 0.5rem;
  position: absolute;
  transform: translateY(-100%);
}

.flip-icon {
  position: absolute;
  bottom: 0.5rem;
  right: 0.5rem;
  font-size: 2.2rem;
  color: white;
  opacity: 0.8;
}

.flip-card-bagside {
  background: white;
  transform: rotateY(180deg);
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 1.5rem;
  color: black;
  text-align: center;
}

.aktOverskrift {
  text-align: center;
  margin-top: 2rem;
  color: #154B82;
}

.aktParagraph {
  text-align: center;
  margin: 2rem 20rem;
  color: #154B82;
}

/* FAQ styling */
.faq-section {
  max-width: 1200px;
  margin: 4rem auto;
  padding: 0 2rem;
}

.faq-title {
  text-align: center;
  margin-bottom: 2rem;
  color: #154B82;
}

.faq-item {
  border: 2px solid #154B82;
  background: #e9ecef;
  margin-bottom: 1rem;
  cursor: pointer;
}

.faq-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1.2rem;
  font-size: 1.1rem;
  color: #154B82;
}

.chevron {
  font-size: 1.6rem;
  transition: transform 0.3s ease;
}

.chevron.open {
  transform: rotate(180deg);
}

.faq-content {
  padding: 1rem 1.2rem 1.5rem;
  background: #ffffff;
  color: #154B82;
}
</style>
