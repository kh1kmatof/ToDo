<template>
    <header class="header">
        <nav class="nav" v-if="!search">
            <button class="nav-lang" @click="switchLang">{{ $i18n.locale }}</button>
            <h3 class="nav-title">{{ $t("note") }}</h3>
            <button @click="showSearch" class="nav-search">
                <img src="@/assets/images/search.svg" alt="">
            </button>
        </nav>
        <nav class="nav_search" v-else>
            <button @click="showSearch" class="nav_search-arrow">
                <img src="@/assets/images/arrow.svg" alt="">
            </button>
            <div class="container">
                <input v-model="searchInp" class="nav_search-input" type="text" placeholder="Qidirish...">
            </div>
            <button v-if="searchInp" @click="clearInput()" class="nav_search-delete">
                <img src="@/assets/images/delete.svg" alt="">
            </button>
        </nav>
    </header>
</template>

<script>
export default {
    data() {
        return {
            search: false,
            searchInp: ''
        }
    },

    methods: {
        showSearch() {
            this.search = !this.search
            this.clearInput()
        },
        clearInput() {
            this.searchInp = ''
        },
        switchLang() {
            this.$i18n.locale == 'RU'
                ? (this.$i18n.locale = 'UZ')
                : (this.$i18n.locale = 'RU');

            localStorage.lang = this.$i18n.locale
        }
    },

    watch: {
        searchInp(newVal) {
            this.$emit("setSearch", newVal)
        }
    }
}
</script>

<style></style>