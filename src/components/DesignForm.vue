<template>
    <form class="design-form">
        <div class="design-form__name">
            <span class="design-form__name-text">
                Who this prayer is for:
            </span>
            <input v-model="name" class="design-form__name-input">
        </div>
        <div class="design-form__room-type">
            <span class="design-form__room-text">
                I want a prayer for
            </span>
            <select v-model="selectedType">
                <option v-for="(type, index) in alphaType" :key="index">{{type}}</option>
            </select>
        </div>
        <fieldset class="design-form__room-tags">
            <legend class="design-form__room-tags-legend">Select your moods:</legend>
            <div class="design-form__room-tags-list">
                <div class="design-form__room-tags-list-item" v-for="(tag, index) in tags" :key="index">
                    <input type="checkbox" :name="tag" :value="tag" :id="tag" v-model="selectedTags">
                    <label :for="tag">
                        <span>{{tag}}</span>
                    </label>
                </div>
            </div>
        </fieldset>
        <div class="design-form__user-input">
            <span class="deisgn-form__user-text">Additional information:</span>
            <textarea v-model="userInput"></textarea>
        </div>
        <div class="design-form__button-wrapper">
            <button
                class="design-form__button-submit"
                @click.prevent="submitPrompt(textPrompt, name, selectedType, selectedTags, userInput)"
                :disabled="isDisabled">
                Generate
            </button>
            <div class="design-form__button-reset-wrapper">
                <a href="#" @click.prevent="reset" class="design-form__button-reset">Reset</a>
            </div>
        </div>
    </form>
</template>

<script>

    export default {
        name: "DesignForm",
        props: ["submitPrompt"],
        data() {
            return {
                type: ["Affirmation", "Absolution", "Thanksgiving", "Adoration", "Intercession", "Supplication", "Guidance", "Prophetic", "Fellowship"],
                tags: [
                    "contemplative",
                    "meditative",
                    "reflective",
                    "confessional",
                    "grateful",
                    "praise-filled",
                    "surrendering",
                    "penitent",
                    "repentant",
                    "devotional",
                    "reverent",
                    "joyful",
                    "healing",
                    "spiritual",
                    "poetic",
                    "metaphorical"
                ],
                name: "",
                selectedType: null,
                selectedTags: [],
                prompt: null,
                userInput: ""
            }
        },
        computed: {
            alphaType() {
                return this.alphaSort(this.type)
            },
            alphaTags() {
                return this.alphaSort(this.tags)
            },
            isDisabled() {
                return !this.selectedType;
            },
            textPrompt() {
                let prompt = `I would like you to write a humanist prayer that is 2 paragraphs long. It should not be overtly religious, nor should it use any explicit religious terminology like God, Buddha, Allah, etc. but should be generically spiritual. This prayer should affirm the reader in their innate value and that they are loved and cared for by the universe.This prayer should be addressed to The Universe and be for a person named ${this.name}. It should be a prayer of ${this.selectedType} with the following qualities: ${this.selectedTags.join(", ")}.`

                if (this.userInput) {
                    prompt += ` Here is additional context for the prayer: ${this.userInput}`;
                }

                return prompt;
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
            reset() {
                this.selectedType = null;
                this.selectedTags = [];
                this.userInput = "";
                this.name = "";
                this.$emit('resetForm')
            },
            toggleTag(event) {
                const tag = event.target.value;
                if (this.selectedTags.includes(tag)) {
                    this.selectedTags = this.selectedTags.filter(el => el !== tag);
                } else {
                    this.selectedTags.push(tag);
                }
            },
        }
    }
</script>

<style>
    .design-form__name {
        margin-bottom: 1rem;
    }
    .design-form__room-text {
        font-weight: bold;
    }

    .design-form__room-tags {
        border: none;
        margin: 2rem 0;
    }

    .design-form__room-tags-legend {
        font-weight: bold;
        text-align: left;
    }

    .design-form__room-tags-list-item {
        margin: 4px;
        color: #000;
        font-weight: bold;
        border-radius: 8px;
        overflow: hidden;
        float: left;
    }

    .design-form__room-tags-list {
        display: grid;
        grid-template-columns: 1fr 1fr 1fr;

    }
    @media (min-width: 50em) {
        .design-form__room-tags-list {
            grid-template-columns: 1fr 1fr 1fr 1fr 1fr;
        }
    }

    .design-form__room-tags-list-item label {
        line-height: 3.0em;
        width: 100%;
        height: 3.0em;
        background-color: #dcde7d;
        display: inline-block;

    }

    @media (min-width: 50em) {
        .design-form__room-tags-list-item label {
            width: 8em
        }
    }

    .design-form__room-tags-list-item input + label:hover {
        background-color: #a8de7d;
    }

    .design-form__room-tags-list-item input:checked + label {
        background-color: #a8de7d;
    }

    .design-form__room-tags-list-item input:checked + label:hover {
        background-color: #72c068;
    }

    .design-form__room-tags-list-item label span {
        text-align: center;
        padding: 3px 0;
        display: block;
    }

    .design-form__room-tags-list-item input {
        clip: rect(0 0 0 0);
        clip-path: inset(50%);
        height: 1px;
        overflow: hidden;
        position: absolute;
        white-space: nowrap;
        width: 1px;
    }

    .design-form__user-input {
        display: flex;
        flex-direction: column;
        padding: 0 2rem 2rem;
    }

    .design-form__user-input textarea {
        display: block;
    }

    .design-form__button-wrapper {
        text-align: center;
    }

    .design-form__button-submit {
        background-color: #5bad4d;
        border-radius: 4px;
        border: none;
        color: #FFF;
        font-weight: bold;
        padding: 1rem 2rem;
        text-transform: uppercase;
        font-size: 1.25rem;
        cursor: pointer;
    }

    .design-form__button-submit:hover {
        background-color: #348425;
        transition: background-color .3s;
    }

    .design-form__button-submit:disabled {
        background-color:#aaaaaa;
        color: #2c3e50;
        cursor: auto;
    }

    .design-form__button-reset-wrapper {
        margin-top: 1rem;
    }

    .design-form__button-reset {
        color: #000;
        font-weight: bold;
    }

    .design-form__button-reset-wrapper {
        text-align: right;
        padding-right: 2rem;
    }
</style>
