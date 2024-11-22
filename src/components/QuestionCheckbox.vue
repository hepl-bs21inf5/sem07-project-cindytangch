<script setup lang="ts">
import { ref, watch, computed, type PropType } from 'vue'

const model = defineModel<boolean>()
const props = defineProps({
  id: { type: String, required: true },
  text: { type: String, required: true },
  answer: {
    type: Array as PropType<Array<string>>,
    required: true,
  },
  options: {
    type: Array as PropType<Array<{ value: string; text: string }>>,
    required: true,
  },
})

const value = ref<string[]>([])
const answer = computed<string>(() => {
  return Object.values(props.answer).sort().toString()
})

watch(
  value,
  newValue => {
    model.value = newValue.sort().toString() === answer.value
  },
  { immediate: true },
)
</script>

<template>
  {{ props.text }}
  <div v-for="option in props.options" :key="option.value" class="form-check">
    <input
      :id="`${props.id}-${option.value}`"
      v-model="value"
      class="form-check-input"
      type="checkbox"
      :name="props.id"
      :value="option.value"
    />
    <label class="form-check-label" :for="`${props.id}-${option.value}`">
      {{ option.text }}
    </label>
  </div>
</template>
