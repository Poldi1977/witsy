
<template>
  <div>
    <div class="group">
      <label>OpenAI Model</label>
      <select v-model="model" @change="save">
        <option v-for="model in models" :key="model.id" :value="model.id">
          {{ model.label }}
        </option>
      </select>
    </div>
    <div class="group">
      <label>OpenAI Voice</label>
      <select v-model="voice" @change="save">
        <option v-for="voice in voices" :key="voice.id" :value="voice.id">
          {{ voice.label }}
        </option>
      </select>
    </div>
    <div class="group">
      <label></label>
      <span>Make sure you enter your OpenAI API key in the Models pane.</span>
    </div>
  </div>
</template>

<script setup lang="ts">

import { ref } from 'vue'
import { store } from '../services/store'

const voice = ref(null)
const model = ref(null)

const models = [
  { id: 'tts-1', label: 'TTS 1' },
  { id: 'tts-1-hd', label: 'TTS 1 HD' },
]

const voices = [
  { id: 'alloy', label: 'Alloy' },
  { id: 'echo', label: 'Echo' },
  { id: 'fable', label: 'Fable' },
  { id: 'onyx', label: 'Onyx' },
  { id: 'nova', label: 'Nova' },
  { id: 'shimmer', label: 'Shimmer' },
]

const load = () => {
  model.value = store.config.engines.openai.tts?.model || 'tts-1'
  voice.value = store.config.engines.openai.tts?.voice || 'alloy'
}

const save = () => {
  store.config.engines.openai.tts.model = model.value
  store.config.engines.openai.tts.voice = voice.value
  store.saveSettings()
}

defineExpose({ load })

</script>

<style scoped>
@import '../../css/dialog.css';
@import '../../css/tabs.css';
@import '../../css/form.css';
</style>
