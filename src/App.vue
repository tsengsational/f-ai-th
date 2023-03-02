<template>
  <div class="interior-desaign">
    <h2>Interior Des[AI]gn</h2>
    <DesignForm :submitPrompt="submitPrompt" />
  </div>
</template>

<script>
import DesignForm from './components/DesignForm.vue';

export default {
  name: 'App',
  components: {
    DesignForm
  },
  methods: {
    async submitPrompt(payload) {
      const response = await fetch('https://api.openai.com/v1/images/generations', {
        method: "POST",
        headers: {
          "Content-Type": "application/json"
        },
        body: payload
      })
      return response.json();
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
