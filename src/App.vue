<template>
  <div class="interior-desaign">
    <h2>Interior Des[AI]gn</h2>
    <DesignForm :submitPrompt="submitPrompt" />
    <results-container :inspirationUrl="inspirationUrl" />
  </div>
</template>

<script>
import DesignForm from './components/DesignForm.vue';
import ResultsContainer from './components/ResultsContainer.vue';

export default {
  name: 'App',
  components: {
    DesignForm,
    ResultsContainer
  },
  data() {
    return {
      inspiration: null
    }
  },
  computed: {
    inspirationUrl() {
      if (this.inspiration) {
        return this.inspiration.data[0].url
      }
      else {
        return ""
      }
    }
  },
  methods: {
    async submitPrompt(textPrompt) {
      const payload = {
        prompt: textPrompt,
        n: 1,
        size: "512x512"
      }

      const response = await fetch('https://api.openai.com/v1/images/generations', {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          "Authorization": `Bearer ${process.env.VUE_APP_OPENAI_API_KEY}`
        },
        body: JSON.stringify(payload)
      })
      let fulfilledResponse = await response.json()
      this.inspiration = await fulfilledResponse
      console.log(this.inspiration)
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
