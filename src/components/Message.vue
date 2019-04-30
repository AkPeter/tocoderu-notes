<template>
    <div class="message" v-if="message">
        {{message}}
    </div>
</template>

<script>

export default {
    props: {
        message: {
            type: String,
            required: true,
            default: 'default message',
        }
    }
}

</script>

<style lang="scss" scoped>
.message {
    padding: 15px 0;
    color: #f00;
}
</style>

