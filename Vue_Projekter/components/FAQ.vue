<script setup>

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

<section class="faq-section">
    <h2 class="faq-title">FAQ</h2>

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

</template>

<style scoped>

.faq-section {
  max-width: 60%;
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