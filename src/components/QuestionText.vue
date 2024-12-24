<script setup lang="ts">
import { ref, watch, type PropType } from 'vue'
import { QuestionState } from '@/utils/models'

const model = defineModel<QuestionState>()
const props = defineProps({
  id: { type: String, required: true },
  text: { type: String, required: true },
  answer: {
    type: Array as PropType<Array<string>>,
    required: true,
  },
  placeholder: { type: String, required: true },
})

const value = ref<string>('')

watch(
  value,
  newValue => {
    model.value = newValue === '' ? QuestionState.Empty : QuestionState.Fill
  },
  { immediate: true },
)

watch(model, newModel => {
  if (newModel === QuestionState.Submit) {
    model.value = props.answer.includes(value.value)
      ? QuestionState.Correct
      : QuestionState.Wrong
  } else if (newModel === QuestionState.Empty) {
    value.value = ''
  }
})
</script>

<template>
  {{ props.text }}
  <div class="form-label">
    <input
      :id="props.id"
      v-model="value"
      class="form-control"
      :placeholder="props.placeholder"
      :disabled="
        model === QuestionState.Submit ||
        model === QuestionState.Correct ||
        model === QuestionState.Wrong
      "
    />
  </div>
</template>
