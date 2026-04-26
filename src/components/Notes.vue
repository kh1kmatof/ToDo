<template>
    <main class="main">
        <div class="container">
            <div class="main_title" v-if="notes.length">
                <h2 class="main-title">{{ $t("allNotes") }}</h2>
                <button @click="show()" class="main-button" :key="toggle">
                    <img v-if="toggle" src="@/assets/images/bar.svg" alt="">
                    <img v-else class="main-button-img" src="@/assets/images/bar2.svg" alt="">
                    <span class="main-button-span">
                        {{ toggle ? $t("list") : $t("set") }}
                    </span>
                </button>
            </div>
            <div v-else-if="searchActive" class="notes_length">
                <p>{{ $t("dont") }}</p>
            </div>
            <div v-else class="notes_length">
                <button @click="$emit('openModal')">{{ $t("clickNote") }}</button>
            </div>
            <div :class="toggle ? 'cards' : 'cards-flex'">
                <Note :toggle="toggle" v-for="note in notes" :key="note.id" :note="note"
                    @dellNote="$emit('dellNote', note.id)" @change="$emit('change', note.id)" />
            </div>
        </div>
    </main>
</template>

<script>
import Note from './Note.vue';

export default {
    data() {
        return {
            toggle: true,
            toggle: JSON.parse(localStorage.getItem('viewType') || 'true')

        }
    },
    methods: {
        show() {
            this.toggle = !this.toggle
            localStorage.setItem('viewType', JSON.stringify(this.toggle))

        }
    },
    components: {
        Note
    },
    props: {
        notes: Array,
        searchActive: Boolean
    }

}
</script>

<style></style>