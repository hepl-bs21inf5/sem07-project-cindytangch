<script setup lang="ts">
import { ref, watch, type PropType } from 'vue'

const model = defineModel<boolean>()
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
    model.value = props.answer.includes(newValue)
  },
  { immediate: true },
)
</script>

<template>
  {{ props.text }}
  <div class="form-label">
    <input
      :id="props.id"
      v-model="value"
      class="form-control"
      :placeholder="props.placeholder"
    />
  </div>
</template>
