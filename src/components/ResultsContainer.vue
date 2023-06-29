<template>
    <div class="results-container" >
        <h2 class="results-container__title">Your Prayer:</h2>
        <div v-show="loading" class="spinner"></div>
            {{ inspirationText }}
        <div v-show="loaded" class="results-image">

        </div>
    </div>
</template>

<script>
export default {
    name: "ResultsContainer",
    props: ["inspirationText", "loading", "loaded", "selectedRoom", "selectedTags"]
}
</script>

<style>
.results-container {
    padding: 3rem 2rem 0;
    white-space: pre-wrap;
    text-align: left
}

.results-container__title {
    margin-bottom: 2rem;
}

.results-image img {
    width: 100%;

}

@media (min-width: 50em) {
    .results-image img {
        width: 32rem;
    }
}

.spinner {
  border: 16px solid #f3f3f3; /* Light grey */
  border-top: 16px solid #a8de7d; /* Blue */
  border-radius: 50%;
  width: 120px;
  height: 120px;
  animation: spin 2s linear infinite;
  margin: 2rem auto 0;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}
</style>

