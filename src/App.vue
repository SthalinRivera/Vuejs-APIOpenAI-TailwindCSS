<script setup>
import { ref, nextTick } from 'vue'
import Footer from './components/Footer.vue';

const content = ref('')
const BTN_TEXT = 'Generar'
const res = ref('✅ La respuesta se mostrará aquí.')
const btnText = ref(BTN_TEXT)

async function createCompletionsChat() {
  try {
    btnText.value = 'Generando'

    const userMessages = [{ role: 'user', content: content.value }]

    const requestData = JSON.stringify({
      model: 'gpt-3.5-turbo',
      messages: userMessages,
      stream: true,
    })

    const fetchOptions = {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        Authorization: `Bearer ${import.meta.env.VITE_OPEN_API_KEY}`,
      },
      body: requestData,
    }

    const response = await fetch('https://api.openai.com/v1/chat/completions', fetchOptions)
    const reader = response.body.getReader()
    res.value = ''

    while (true) {
      const { done, value } = await reader.read()
      if (done) break

      const chunkStr = new TextDecoder('utf-8').decode(value)
      const lines = chunkStr
        .split('\n')
        .filter((line) => line !== '' && line.length > 0)
        .map((line) => line.replace(/^data: /, '').trim())
        .filter((line) => line !== '[DONE]')
        .map((line) => JSON.parse(line))
      for (const line of lines) {
        const {
          choices: [
            {
              delta: { content },
            },
          ],
        } = line
        if (content) {
          res.value += content
        }
      }
    }
    console.log('Stream ended.')
  } catch (error) {
    console.error(error)
    res.value = error.response.data.error.message
  } finally {
    btnText.value = BTN_TEXT
  }
}

const askAi = () => {
  createCompletionsChat()
}
</script>

<template>

  <h2 class="text-2xl font-bold text-center text-gray-800 mb-4">Vue js , Open AI y Tailwind CSS</h2>
  <div class="p-6 max-w-md mx-auto bg-white rounded-lg shadow-lg">
    <h2 class="text-2xl font-bold text-center text-gray-800 mb-4"> Generador de post para Redes sociales</h2>

    <div class="mb-4">
      <input
        class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-indigo-500"
        placeholder="Pregúntame sobre..." v-model="content" clear />
    </div>

    <div class="mb-4 flex justify-center">
      <button type="button" @click="askAi"
        class="relative px-6 py-3 bg-indigo-600 text-white font-semibold rounded-lg shadow-md transition-transform transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-indigo-500">
        <strong>{{ btnText }}</strong>
        <div id="container-stars" class="absolute inset-0 flex items-center justify-center pointer-events-none">
          <div id="stars" class="absolute w-full h-full bg-gradient-to-r from-transparent to-yellow-500 opacity-20">
          </div>
        </div>

      </button>
    </div>
    <div class="bg-gray-100 p-4 rounded-lg shadow-inner">
      <pre class="whitespace-pre-wrap text-gray-800">{{ res }}</pre>
    </div>
  </div>
  <Footer />
</template>


<style scoped></style>