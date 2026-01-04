<script setup>
import { ref } from 'vue';

// steps
const step = ref(1)

// steps data
const formData = ref({
    name: '',
    lastName: '',
    email: '',
    telefonNr: '',
    date: '',
    time:'',
    antalDeltagere: '',

})



// navigere steps
const nextStep = () => {
    if (step.value < 5) step.value++
}

const prevStep = () => {
    if (step.value > 1) step.value--
}

// submit form
const sumbitForm = () => {
    console.log("Din booking er nu insendt!", formData.vaule)
}

// dropdown til tilbudspakker
const valgtTilbud = ref("")
const tilbudspakker = [
    "Action (10min Gokart, 12min Lasergame, 57min Bowling)",
    "Lux Action(25min Gokart, 20min Lasergame, 57min Bowling)",
    "Mega Action(55min Gokart, 30min Lasergame, 117min Bowling)",
    "Formel 1(25min Gokart inkl. (15mins tidstagning, 10min Finale))",
    "Lux Formel 1(50min Gokart inkl. (25min tidstagning, 25min Finale))",
    "Leman (50min holdkørsel - min 16 hold)",
    "Herre Aften (25min Gokart, 57min Bowling, skydesimulator)",
    "Dame aften (20min Lasergame, 57min Bowling, skydesimulator)",
    "Blå Mandags pakke",
    "Julefrokost",
    "Spis & Bowl(spisning, 57min Bowling)",
    "Børnefødselsdag",
    "Vr Action pakke(10min Gokart, 12min VR, 12min Lasergame)",
    "Lux VR Action pakke(24min VR, 25min Gokart, 20min Lasergame)"
]

const valgtAktivitet = ref([])
const aktiviteter = [
  "Bowling",
  "10min Gokart",
  "15min Gokart",
  "Formel 1(gokart 25min)",
  "Lux Formel 1(gokart 50min)",
  "12min Lasergame",
  "20min Lasergame",
  "30min Lasergame",
  "Legeland",
  "30min skydesimulator",
  "60min skydesimulator",
  "12min Virtuel reality (min 12 år)",
  "24min Virtuel reality (min 12 år)"
]

const valgtSpiseOpt = ref([])
const spiseOpt = [
  "forret",
  "hovedret",
  "buffet",
  "frisoftice til buffet",
  "dessert"
]

// checkbox visning
const visAktivitet = ref(false)
const visTilbud = ref(false)
</script>

<template>
 <div class="booking-form">

    <!-- dette er en progress bar, den virker på den måde at du har en span med class det svarer til et step i booking formularen, ved at indlæse det index man er inde på. når du er inde på et step i booking formularen får det en active class, og på den måde kan identifiecere hvilket step der skal fremvises på grænsefladen -->
    <div class="steps">
      <span :class="{ active: step === 1 }">1</span>
      <span :class="{ active: step === 2 }">2</span>
      <span :class="{ active: step === 3 }">3</span>
      <span :class="{ active: step === 4 }">4</span>
      <span :class="{ active: step === 5 }">5</span>
    </div>

    <!-- Step 1 -->
    <div class="step" v-if="step === 1">
      <h2>Person Oplysninger</h2>
      <label for="fornavn">Fornavn</label>
      <br>
      <input type="text" placeholder="fornavn" v-model="formData.name" />
      <br>
      <label for="efternavn">Efternavn</label>
      <br>
      <input type="text" placeholder="efternavn" v-model="formData.lastName" />
      <br>
      <label for="Email">Email</label>
      <br>
      <input type="email" placeholder="ActionHouse@actionhouse.dk" v-model="formData.email">
      <br>
      <label for="telefon">Telefon nr</label>
      <br>
      <input type="tel" placeholder="+45 00 00 00 00" v-model="formData.tel">
      <button @click="nextStep">Næste</button>
    </div>

    <!-- Step 2 -->
    <div class="step" v-if="step === 2">
      <h2>Dato og Tid</h2>
      <label for="dato">Dato</label>
      <br>
      <input type="date" v-model="formData.date">
      <br>
      <label for="time">Tidspunkt</label>
      <br>
      <input type="time" v-model="formData.time">
      <br>
      <label for="Deltager">Antal Deltager</label>
      <br>
      <input type="text" v-model="formData.antalDeltagere">
      <div>
          <button @click="prevStep">Tilbage</button>
          <button @click="nextStep">Næste</button>
      </div>
    </div>

    <!-- Step 3 -->
    <div class="step" v-if="step === 3">
      <h2>Valg af Aktivitet</h2>
      <div class="checkboxContainer">
        <div>
          <label for="vælgTilbudspakker">tilbudspakker</label>
          <input type="checkbox" id="vælgTilbudspakke" v-model="visTilbud">
          <br>
          <br>
          <select v-if="visTilbud" name="vælgTilbudspakker" id="vælgTilbudspakker" v-model="valgtTilbud">
            <option disabled value="">Vælg et tilbud</option>
            <option v-for="tilbudspakke in tilbudspakker" :key="tilbudspakke" value="tilbudspakke">{{ tilbudspakke }}</option>
          </select>
        </div>
        <div> 
          <label for="vælgAktiviteter">Aktiviteter</label>
          <!-- Checkbox der viser/skjuler listen --> 
          <input type="checkbox" id="vælgAktivitet" v-model="visAktivitet">
          <!-- Liste over aktiviteter --> 
          <div v-if="visAktivitet"> 
            <div v-for="aktivitet in aktiviteter" :key="aktivitet">
            <input type="checkbox" :id="aktivitet" :value="aktivitet" v-model="valgtAktivitet" > 
            <label :for="aktivitet">{{ aktivitet }}</label> 
          </div> 
        </div> 
      </div>
      </div>
    <div>
        <button @click="prevStep">Tilbage</button>
        <button @click="nextStep">næste</button>
    </div>
    </div>
    <div class="step" v-if="step === 4">
      <h2>Spisning</h2>
      <div class="spisningContainer">
        <div v-for="food in spiseOpt" :key="food" class="foodContainer">
          <input type="Checkbox" :id="food" :value="food" v-model="valgtSpiseOpt">
          <label :for="food">{{ food }}</label>
        </div>
      </div>
      <div>
        <button @click="prevStep">tilbage</button>
        <button @click="nextStep">Næste</button>
      </div>
    </div>
    <div class="step" v-if="step === 5">
      <div>
        <button @click="prevStep">tilbage</button>
        <button @click="nextStep">næste</button>
      </div>
    </div>
 </div>
</template>

<style scoped>
.steps {
  display: flex;
  gap: 10px;
  justify-content: space-evenly;
}
.steps span {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  background: #ddd;
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 50px;
}
.steps .active {
  background: var(--mainblue);
  color: white;
}

input{
    width: 1000px;
    height: 2rem;
}

.step{
    display: flex;
    flex-direction: column;
    justify-content: center;
    margin-left: 350px;
    margin-right: 350px;
}
.step button{
    width: 100px;
    justify-content: space-between;
    align-items: flex-end;
    margin: 1rem;
}



.checkboxContainer { 
  display: flex;
  gap: 15px; 
  padding: 20px; 
  justify-content: space-between;
  
}


.checkboxContainer input[type="checkbox"] { 
  margin-right: 10px;  
  width: 50px;
  } 
    
.checkboxContainer select { 
  padding: 10px 12px; 
  background: white; 
  font-size: 15px; 
} 
.spisningContainer { 
  display: flex;
  gap: 15px; 
  padding: 20px; 
  justify-content: space-evenly;
  flex-direction: column;
  
}


.spisningContainer input[type="checkbox"] { 
  margin-right: 10px;  
  width: 50px;
  } 
    
.spisningContainer select { 
  padding: 10px 12px; 
  background: white; 
  font-size: 15px; 
} 

      












</style>