<template>
    <form class="design-form">
        <div class="design-form__room-type">
            <span class="design-form__room-text">
                I'm designing a
            </span>
            <select v-model="selectedRoom" >
                <option v-for="(room, index) in alphaRooms" :key="index">{{ room }}</option>
            </select>
        </div>
        <div class="design-form__room-tags">
            <ul class="design-form__room-tags-list">
                <li class="design-form__room-tags-list-item" v-for="(tag, index) in tags" :key="index">
                    <input type="checkbox" :name="tag" :value="tag" @change="toggleTag" :checked="selectedTags.includes(tag)">
                    <label :for="tag">{{ tag }}</label>
                </li>
            </ul>
        </div>
        <button @click.prevent="submitPrompt(textPrompt, selectedRoom, selectedTags)">Generate</button>
        <a href="#" @click.prevent="reset" >Reset</a>
    </form>
</template>

<script>

export default {
    name: "DesignForm",
    props: ["submitPrompt"],
    data() {
        return {
            rooms: ["Kitchen", "Living Room", "Bed Room", "Study", "Bath Room", "Dining Room", "Entry Way", "Teen Girls Room", "Teen Boys Room", "Kids Room", "Nursery", "Home Office", "Home Library", "Balcony", "Patio", "Vanity Room"],
            tags: ["Bohemian", "Concrete", "Minimalist", "Maximalist", "Midcentury", "Grandmillennial", "Traditional", "Japandi", "Scandinavian", "European", "Mediterranian", "Victorian", "Serious", "Playful", "Vibrant", "Organic", "Farmhouse", "Classic", "Luxurious", "Japanese", "Feng Shui", "Vintage", "Contemporary", "Industrial", "Monochromatic"],
            selectedRoom: null,
            selectedTags: [],
            prompt: null
        }
    },
    computed: {
        alphaRooms() {
            return this.alphaSort(this.rooms)
        },
        alphaTags() {
            return this.alphaSort(this.tags)
        },
        textPrompt() {
            return `magazine spread photograph of a ${this.selectedRoom} with ${this.selectedTags.join(", ")} style, high def, atmospheric lighiting, dynamic lighting`
        }
    },
    methods: {
        alphaSort(arr) {
            return [...arr].sort((a, b) => {
                if (a < b) {
                    return -1;
                }
                if (a > b) {
                    return 1;
                }
                return 0;
            })
        },
        reset(){
            this.selectedRoom = null;
            this.selectedTags = []
            this.$emit('resetForm')
        },
        toggleTag(event) {
            const tag = event.target.value;
            if (this.selectedTags.includes(tag)) {
                this.selectedTags = this.selectedTags.filter( el => el !== tag );
            } else {
                this.selectedTags.push(tag);
            }
        }
    }
}
</script>
