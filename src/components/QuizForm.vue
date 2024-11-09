<script setup lang="ts">
import { computed, ref } from 'vue'

const q1 = ref<string | null>(null)
const q2 = ref<string | null>(null)
const q3 = ref<string | null>(null)
const filled = computed<boolean>(
  () => q1.value !== null && q2.value !== null && q3.value !== null,
)

function submit(event: Event): void {
  event.preventDefault()
  const count = ref<number>(0)

  const n_questions = 3
  if (q1.value === 'a11') {
    count.value += 1
  }
  if (q2.value === 'a21') {
    count.value += 1
  }
  if (q3.value === 'a33') {
    count.value += 1
  }
  if (filled.value) {
    alert(`Score : ${count.value}/${n_questions}`)
    if (count.value === n_questions) {
      alert(`Bravo !`)
    }
  }
}

function reset(): void {
  q1.value = null
  q2.value = null
  q3.value = null
}
</script>

<template>
  <form @submit="submit">
    <!-- Q1 -->
    Le marcophage est ...
    <div class="form-check">
      <input
        id="a11"
        v-model="q1"
        class="form-check-input"
        type="radio"
        name="q1"
        value="a11"
      />
      <label class="form-check-label" for="a11"
        >une cellule de l'immunité innée.</label
      >
    </div>
    <div class="form-check">
      <input
        id="a12"
        v-model="q1"
        class="form-check-input"
        type="radio"
        name="q1"
        value="a12"
      />
      <label class="form-check-label" for="a12"
        >une cellule de l'immunité adaptative.</label
      >
    </div>
    <div class="form-check">
      <input
        id="a13"
        v-model="q1"
        class="form-check-input"
        type="radio"
        name="q1"
        value="a13"
      />
      <label class="form-check-label" for="a13">un événement.</label>
    </div>
    <div class="form-check">
      <input
        id="a14"
        v-model="q1"
        class="form-check-input"
        type="radio"
        name="q1"
        value="a14"
      />
      <label class="form-check-label" for="a14">un événement final.</label>
    </div>

    <!-- Q2 -->
    Quelles cellules effectuent la phagocytose ?
    <div class="form-check">
      <input
        id="a21"
        v-model="q2"
        class="form-check-input"
        type="radio"
        name="q2"
        value="a21"
      />
      <label class="form-check-label" for="a21"
        >Les cellules dendritiques.</label
      >
    </div>
    <div class="form-check">
      <input
        id="a22"
        v-model="q2"
        class="form-check-input"
        type="radio"
        name="q2"
        value="a22"
      />
      <label class="form-check-label" for="a22"
        >Les lymphocytes T cytotoxiques.</label
      >
    </div>
    <div class="form-check">
      <input
        id="a23"
        v-model="q2"
        class="form-check-input"
        type="radio"
        name="q2"
        value="a23"
      />
      <label class="form-check-label" for="a23"
        >Les lymphocytes T auxiliaires.</label
      >
    </div>
    <div class="form-check">
      <input
        id="a24"
        v-model="q2"
        class="form-check-input"
        type="radio"
        name="q2"
        value="a24"
      />
      <label class="form-check-label" for="a24">Les anticorps.</label>
    </div>

    <!-- Q3 -->
    Le lymphocyte T cytotoxique...
    <div class="form-check">
      <input
        id="a31"
        v-model="q3"
        class="form-check-input"
        type="radio"
        name="q3"
        value="a31"
      />
      <label class="form-check-label" for="a31">produit des anticorps.</label>
    </div>
    <div class="form-check">
      <input
        id="a32"
        v-model="q3"
        class="form-check-input"
        type="radio"
        name="q3"
        value="a32"
      />
      <label class="form-check-label" for="a32">phagocyte la pathogène.</label>
    </div>
    <div class="form-check">
      <input
        id="a33"
        v-model="q3"
        class="form-check-input"
        type="radio"
        name="q3"
        value="a33"
      />
      <label class="form-check-label" for="a33"
        >libère des perforines et granzymes.</label
      >
    </div>
    <div class="form-check">
      <input
        id="a34"
        v-model="q3"
        class="form-check-input"
        type="radio"
        name="q3"
        value="a34"
      />
      <label class="form-check-label" for="a34">libère des cytokines.</label>
    </div>

    <button
      class="btn btn-primary"
      :class="{ disabled: !filled }"
      type="submit"
    >
      Terminer
    </button>
  </form>
  <button class="btn btn-secondary" @click="reset">Réinitialiser</button>
</template>
