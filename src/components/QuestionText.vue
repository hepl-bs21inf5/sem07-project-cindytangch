<script setup lang="ts">
import { defineModel, defineProps } from 'vue'

const model = defineModel<string | null>()
const props = defineProps({
  id: { type: String, required: true },
  text: { type: String, required: true },
  placeholder: { type: String, required: true },
})
</script>

<template>
  {{ props.text }}
  <div class="form-label">
    <input
      :id="props.id"
      v-model="model"
      class="form-control"
      :placeholder="props.placeholder"
    />
  </div>
</template>
