<template>
    <div class="interior-desaign__recirc">
        <h2 v-show="showRecirc">More Inspirations:</h2>
        <div
            v-show="showRecirc"
            v-for="(article, index) in filteredArticles"
            :key="index"
            class="interior-desaign__recirc-article">
            <a class="recirc-article__link" :href="article.Url">
                <div class="recirc-article__image-container">
                    <img :src="article['Primary Image']" />
                </div>
                <h3 class="recirc-article__title">
                    {{ article.Title }}
                </h3>
            </a>
        </div>
    </div>
</template>

<script>
import dummyData from './DummyData'

export default {
    name: "RecircContainer",
    props: ["selectedRoom", "selectedTags"],
    data() {
        return {
            articles: dummyData
        }
    },
    computed: {
        filteredArticles() {
            return dummyData.filter( article => article.Room == this.selectedRoom)
        },
        showRecirc() {
            return this.filteredArticles.length > 0;
        }
    }
}
</script>

<style scoped>
.interior-desaign__recirc {
    background-color: #C0E2AF;
    padding: 2rem;
    margin-top: 3rem;
}

.interior-desaign__recirc-article {
    margin-bottom: 1rem;
    padding: .75rem;
    background-color: #f0f7e3;
}

.recirc-article__link {
    display: flex;
    flex-direction: row;
    text-decoration: none;
    text-align: left;
}

.recirc-article__image-container img {
    width: 7.5rem;
    height: 7.5rem;
    object-fit: cover;
    margin-right: 1.5rem;
}

.recirc-article__title {
    color: #2c3e50;
    font-size: 1.5rem;
}
</style>
