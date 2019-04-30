<template>
    <div class="new-note">
        <div class="new-note__title-satus">
            <input v-model="note.title" type="text">
            <select class="select" v-model="note.selected">
                <option v-for="item in note.statuses" :key="item.value" v-bind:value="item.value">{{item.text}}</option>
            </select>
        </div>
        <textarea v-model="note.descr"></textarea>
        <button class="btn btnPrimary" @click="addNote">New note</button>
    </div>
</template>

<script>
export default {
    props: {
        note: {
            type: Object,
            required: true,
        }
    },
    methods: {
        addNote () {
            this.$emit('addNote', this.note)
        }
    }
}
</script>

<style lang="scss" scoped>
.btn {
    margin-top: 20px;
}
.select {
    border: 1px solid #dcdfe6;
    background-color: #fff;
    padding: 15px;
    margin-left: 12px;
    border-radius: 20px;
}
.new-note__title-satus {
    display: flex;
    flex-flow: row nowrap;
    align-items: flex-start;
}
</style>


