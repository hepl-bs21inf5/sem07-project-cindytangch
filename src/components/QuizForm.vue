<script setup lang="ts">
import { computed, ref } from 'vue'
import QuestionRadio from '@/components/QuestionRadio.vue'
import QuestionText from '@/components/QuestionText.vue'
import QuestionCheckbox from '@/components/QuestionCheckbox.vue'

const q1 = ref<string | null>(null)
const q2 = ref<string[]>([])
const q3 = ref<string | null>(null)
const q4 = ref<string | null>(null)
const filled = computed<boolean>(
  () => q1.value !== null && Object.keys(q2).length !== 0 && q3.value !== null,
)

function submit(event: Event): void {
  event.preventDefault()
  const count = ref<number>(0)

  const n_questions = 3
  if (q1.value === 'a11') {
    count.value += 1
  }
  if (
    Object.values(q2.value).sort().toString() ===
    ['a21', 'a24'].sort().toString()
  ) {
    count.value += 1
  }
  if (q3.value === 'a32') {
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
  q2.value = []
  q3.value = null
  q4.value = null
}
</script>

<template>
  <form @submit="submit">
    <QuestionRadio
      id="q1"
      v-model="q1"
      text="Le marcophage est ..."
      :options="[
        { value: 'a11', text: 'une cellule de l\'immunité innée.' },
        { value: 'a12', text: 'une cellule de l\'immunité adaptative.' },
        { value: 'a13', text: 'un événement.' },
        { value: 'a14', text: 'un événement final.' },
      ]"
    />
    <QuestionCheckbox
      id="q2"
      v-model="q2"
      text="Quelles cellules effectuent la phagocytose ?"
      :options="[
        { value: 'a21', text: 'La cellule dendritique.' },
        { value: 'a22', text: 'La cellule tueuse naturelle' },
        { value: 'a23', text: 'Le lymphocyte T cytotoxique.' },
        { value: 'a24', text: 'Le macrophage.' },
      ]"
    />
    <QuestionRadio
      id="q3"
      v-model="q3"
      text="Le lymphocyte T cytotoxique..."
      :options="[
        { value: 'a31', text: 'produit des anticorps.' },
        { value: 'a32', text: 'libère des perforines et granzymes.' },
        { value: 'a33', text: 'libère des cytokines.' },
        { value: 'a34', text: 'phagocyte le pathogène.' },
      ]"
    />
    <QuestionText
      id="q4"
      v-model="q4"
      text="Combien de parties avez-vous jouées ?"
      placeholder="Veuillez saisir un nombre"
    />
    <button
      class="btn btn-primary"
      :class="{ disabled: !filled }"
      type="submit"
    >
      Terminer
    </button>
    <button class="btn btn-secondary" @click="reset">Réinitialiser</button>
  </form>
</template>
