
<template>
  <select v-model="value" @change="$emit('change')">
    <option value="" v-if="defaultText">{{ defaultText }}</option>
    <option value="openai">OpenAI</option>
    <option value="ollama">Ollama</option>
    <option value="anthropic">Anthropic</option>
    <option value="mistralai">MistralAI</option>
    <option value="google">Google</option>
    <option value="xai">xAI</option>
    <option value="openrouter">OpenRouter</option>
    <option value="deepseek">DeepSeek</option>
    <option value="groq">Groq</option>
    <option value="cerebras">Cerebras</option>
    <option v-for="c in custom" :key="c.id" :value="c.id">{{ c.label }}</option>
  </select>
</template>

<script setup lang="ts">

import { CustomEngineConfig } from '../types/config'
import { computed } from 'vue'
import { store } from '../services/store'
import LlmFactory from '../llms/llm'

const llmFactory = new LlmFactory(store.config)

defineProps({
  defaultText: String
})

const value = defineModel()
const emit = defineEmits(['change'])

const custom = computed(() => {
  const customs = llmFactory.getCustomEngines()
  return customs.map((id) => ({
    id: id,
    label: (store.config.engines[id] as CustomEngineConfig).label
  }))
})

</script>
