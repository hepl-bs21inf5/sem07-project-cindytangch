<script setup lang="ts">
import QuestionRadio from '@/components/QuestionRadio.vue'
import { reactive, ref, computed } from 'vue'

const questions = ref<
  {
    question: string
    correct_answer: string
    incorrect_answers: string[]
  }[]
>([])
const correctAnswers = ref<boolean[]>([])
const score = computed<number>(
  () => correctAnswers.value.filter(value => value).length,
)
const totalScore = computed<number>(() => correctAnswers.value.length)

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
      v-model="correctAnswers[index]"
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
  <div>Réponses correctes : {{ correctAnswers }}</div>
  <div>Score : {{ score }} / {{ totalScore }}</div>
</template>
