<template>
    <div class="results-container">
        <div class="results-image">
            <img :src="inspirationUrl" >
        </div>
    </div>
</template>

<script>

export default {
    name: "ResultsContainer",
    props: ["inspirationUrl"]
}
</script>

