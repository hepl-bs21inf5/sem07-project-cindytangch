<script setup lang="ts">
import { computed, ref } from 'vue'
import QuestionRadio from '@/components/QuestionRadio.vue'
import QuestionText from '@/components/QuestionText.vue'
import QuestionCheckbox from '@/components/QuestionCheckbox.vue'
import { QuestionState } from '@/utils/models'

const questionStates = ref<QuestionState[]>([])
const filled = computed<boolean>(() =>
  questionStates.value.every(state => state === QuestionState.Fill),
)
const submitted = computed<boolean>(() =>
  questionStates.value.every(
    state => state === QuestionState.Correct || state === QuestionState.Wrong,
  ),
)
const score = computed<number>(
  () =>
    questionStates.value.filter(state => state === QuestionState.Correct)
      .length,
)
const totalScore = computed<number>(() => questionStates.value.length)

function reset(event: Event): void {
  event.preventDefault()
  questionStates.value = questionStates.value.map(() => QuestionState.Empty)
}

function submit(event: Event): void {
  event.preventDefault()
  questionStates.value = questionStates.value.map(() => QuestionState.Submit)
}
</script>

<template>
  <form>
    <QuestionRadio
      id="q1"
      v-model="questionStates[0]"
      answer="a11"
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
      v-model="questionStates[1]"
      :answer="['a21', 'a24']"
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
      v-model="questionStates[2]"
      answer="a33"
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
      v-model="questionStates[3]"
      :answer="['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', '10']"
      text="Combien de parties avez-vous jouées ?"
      placeholder="Veuillez saisir un nombre"
    />
    <button
      class="btn btn-primary"
      :class="{ disabled: !filled }"
      @click="submit"
    >
      Terminer
    </button>
    <button class="btn btn-secondary" @click="reset">Réinitialiser</button>
    <div>Debug états : {{ questionStates }}</div>
    <div v-if="submitted">Score : {{ score }} / {{ totalScore }}</div>
  </form>
</template>
