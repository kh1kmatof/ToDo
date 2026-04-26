<template>
    <Header @setSearch="searchValue = $event" />
    <Notes :notes="filterNotes" @openModal="openModal" @dellNote="dellNote" @change="change" :searchActive="searchValue.length > 0" />
    <AddButton v-if="!showModal" @openModal="openModal" />
    <Transition name="modal">
        <Modal v-if="showModal" @closeModal="closeModal" @addNote="addNote" :edit="edit" :editNote="editNote"
            @changeNote="changeNote" />
    </Transition>
</template>

<script>
import AddButton from './components/AddButton.vue';
import Header from './components/Header.vue';
import Modal from './components/Modal.vue';
import Notes from './components/Notes.vue';


export default {
    components: {
        Header,
        Notes,
        AddButton,
        Modal
    },

    data() {
        return {
            showModal: false,
            edit: false,
            editNote: null,
            notes: [],
            searchValue: ''
        }
    },

    computed: {
        filterNotes() {
            return this.searchValue ? this.notes.filter((note)=> note.title.toLowerCase().includes(this.searchValue.toLowerCase())) : this.notes
        },
    },

    methods: {
        openModal() {
            this.showModal = true
            this.edit = false
        },
        closeModal(status) {
            this.showModal = status
        },
        addNote(note) {
            this.notes.push(note)
            this.showModal = false
        },
        getNotes() {
            let localNotes = localStorage.notes
            if (localNotes) {
                this.notes = JSON.parse(localNotes)
            }
        },
        dellNote(id) {
            let index = this.notes.findIndex((item) => {
                return item.id == id
            });
            this.notes.splice(index, 1)
        },
        change(id) {
            // console.log(id);
            this.showModal = true
            this.edit = true
            let currentNotem = this.notes.find((note) => note.id == id)
            this.editNote = currentNotem

        },
        changeNote(newNote) {
            this.notes.forEach((note) => {
                if (note.id == newNote.id) {
                    note.title = newNote.title || note.title
                    note.text = newNote.text || note.text
                    note.date = newNote.date
                }
            })
            this.closeModal()
        }

    },

    watch: {
        notes: {
            handler() {
                localStorage.notes = JSON.stringify(this.notes)
            },
            deep: true
        }
    },
    mounted() {
        this.getNotes()
    }

}
</script>

<style>
/* we will explain what these classes do next! */
.modal-enter-active,
.modal-leave-active {
    transition: opacity 0.1s ease;
}

.modal-enter-from,
.modal-leave-to {
    opacity: 0;
}
</style>