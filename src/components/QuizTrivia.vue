<script setup lang="ts">
import QuestionRadio from '@/components/QuestionRadio.vue'
import { QuestionState } from '@/utils/models'
import { reactive, ref, computed } from 'vue'

const questions = ref<
  {
    question: string
    correct_answer: string
    incorrect_answers: string[]
  }[]
>([])
const questionStates = ref<QuestionState[]>([])
const score = computed<number>(
  () =>
    questionStates.value.filter(state => state === QuestionState.Correct)
      .length,
)
const totalScore = computed<number>(() => questionStates.value.length)

fetch('https://opentdb.com/api.php?amount=10&type=multiple')
  .then(response => response.json())
  .then(data => (questions.value = data.results))
</script>

<template>
  <form>
    <QuestionRadio
      v-for="(question, index) in questions"
      :id="index.toString()"
      :key="index"
      v-model="questionStates[index]"
      :answer="question.correct_answer"
      :text="question.question"
      :options="[
        { value: question.correct_answer, text: question.correct_answer },
        ...question.incorrect_answers.map(answer => ({
          value: answer,
          text: answer,
        })),
      ]"
    />
  </form>
  <div>Réponses correctes : {{ questionStates }}</div>
  <div>Score : {{ score }} / {{ totalScore }}</div>
</template>
