<template>
    <div class="card">
        <div :class="{ 'card_top': !toggle }">
            <h3 class="card-title">{{ note.title }}</h3>
            <p class="card-time">{{ note.date }}</p>
        </div>
        <p class="card-text">{{ note.text }}</p>
        <div class="card_buttons">
            <button class="card_buttons-remove" @click="$emit('change', note.id)"><img src="@/assets/images/pen.svg" alt="">
                {{ $t("change") }}</button>
            <button class="card_buttons-delete" @click="$emit('dellNote', note.id)"><img src="@/assets/images/rubbish.svg" alt="">
                {{ $t("delete") }}</button>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        toggle: Boolean,
        note: Object
    },
    components: {
    }
}


</script>

<style></style>