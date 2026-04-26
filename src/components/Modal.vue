<template>
    <div class="modal" @click="$emit('closeModal')">
        <div class="modal_about" @click.stop="">
            <h2 class="modal_about-title">{{ edit ? $t("rename") : $t("addNote") }}</h2>
            <div class="modal_about_input">
                <span class="modal_about_input-span">Title</span>
                <input v-model="title" type="text" placeholder="Title" @keyup.enter="addNote">
            </div>
            <div class="modal_about_input">
                <span class="modal_about_input-span">Content</span>
                <input v-model="text" type="text" placeholder="Content" @keyup.enter="addNote">
            </div>
            <div class="modal_about_buttons">
                <button class="modal_about_buttons-cancel" @click="$emit('closeModal')">{{ $t("cancel") }}</button>
                <button class="modal_about_buttons-add" v-if="!edit" @click="addNote()">{{ $t("add") }}</button>
                <button class="modal_about_buttons-add" v-else @click="changeNote">{{ $t("change") }}</button>
            </div>
        </div>
    </div>
</template>

<script>

let id = 0

export default {
    props: {
        edit: Boolean,
        editNote: Object
    },
    data() {
        return {
            title: '',
            text: ''
        }
    },
    methods: {
        addNote() {
            if (this.title != '' && this.text != '') {
                const note = {
                    id: id++,
                    title: this.title,
                    text: this.text,
                    date: new Date().toLocaleTimeString()
                };

                this.title = '',
                    this.text = '',

                    this.$emit('addNote', note)
            }

        },
        changeNote() {
            const newEditedNote = {
                id: this.editNote.id,
                title: this.title,
                text: this.text,
                date: new Date().toLocaleTimeString()
            };
            this.$emit('changeNote', newEditedNote)
        }
    }
}
</script>

<style></style>