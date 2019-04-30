<template>
    <div class="notes">
        <div class="note" :class="[{full: !grid}, 'status status-' + note.selected]" v-for="(note, index) in notes" :key="index">
            <span @click="removeNote(index)" class="note-remove">Remove</span>
            <div class="note-header">
                <p v-if="note.editable" @click="editTitle(note)"> {{note.title}} </p>
                <input 
                    v-if="!note.editable" 
                    ref="title" 
                    v-model="note.title" 
                    @keyup.esc="notUpdateTitle(note)" 
                    @keyup.enter="updateTitle(note)" type="text" />
            </div>
            <div class="note-body">
                <p v-if="note.editable"> {{note.descr}} </p>
                <input 
                    v-if="!note.editable"
                    v-model="note.descr" 
                    @keyup.esc="notUpdateTitle(note)" 
                    @keyup.enter="updateTitle(note)" type="text" />
                <span> {{note.date}} </span>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        notes: {
            type: Array,
            required: true,
        },
        grid: {
            tupe: Boolean,
            required: true,
        }
    },
    data () {
        return {
            //show: true,
        }
    },
    methods: {
        removeNote (index) {
            console.log( `Note id: ${index} - removed` )
            this.$emit('remove', index)
        },
        // editText (index) {
        //     this.$emit('edit', index)
        //     console.log( `Note id: ${index} - edited` )
        // },
        editTitle (note) {
            this.$emit('edit', note)
            //this.$refs.title.focus(note)
            //note.editable = false
            //console.log(note)
        },
        updateTitle (note) {
            this.$emit('update', note)
            //note.editable = true
            //console.log(note)
        },
        notUpdateTitle (note) {
            this.$emit('notupdate', note)
        }
    }
}
</script>

<style lang="scss">
.notes {
    display: flex;
    flex-flow: row wrap;
    justify-content: space-between;
    align-items: flex-start;
}
.note {
    position: relative;
    width: 49%;
    margin-bottom: 20px;
    background-color: #fff;
    border-radius: 6px;
    padding: 20px;

    &.full {
        width: 100%;
    }

    &.status {
        border-left: 2px solid;
        &-1 {
            border-color: aqua;
        }
        &-2 {
            border-color: yellow;
        }
        &-3 {
            border-color: red;
        }
    }

    &-header {
        display: flex;
        flex-flow: row wrap;
        justify-content: space-between;
        align-items: center;
        p {
            font-size: 22px;
            color: darkcyan;
            font-weight: bold;
        }
        svg {
            color: #777;
            margin-right: 12px;
            cursor: pointer;
            &:last-child {
                margin-right: 0;
            }
            &.active {
                color: #000;
            }
        }
    }

    &-body {
        p {
            padding: 15px 0;
        }
        span {
            font-size: 12px;
            color: #777;
        }
    }

    &-remove {
        position: absolute;
        top: 15px;
        right: 15px;
        font-size: 12px;
        cursor: pointer;
        color: #777;
    }
}
</style>

