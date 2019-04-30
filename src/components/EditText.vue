<template>
    <div class="edit-text">
        <span class="edit-text__text"></span>
        <input class="edit-text__input" type="text" />
    </div>
</template>

<script>
export default {
    props: {
        text: {
            type: String,
            required: true,
        }
    },
    methods: {
        editText (index) {
            this.$emit('editText', index)
        }
    }
}
</script>

<style lang="scss" scoped>

</style>


