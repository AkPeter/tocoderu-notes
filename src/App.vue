<template>
  <div class="wrapper">

    <!-- <header></header> -->

    <div class="wrapper-content">
      <section>
        <div class="container">
          
          

          <message v-if="message" :message="message" />

          <newNote :note="note" @addNote="addNote"/>

          <div class="note-header">

            <h1 class="title">{{title}}</h1>

            <search :value="search" @search="search = $event" placeholder="Find note" />

            <div class="icons">
              <svg :class="{ active: grid }" @click="grid = true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" ><rect x="3" y="3" width="7" height="7"></rect><rect x="14" y="3" width="7" height="7"></rect><rect x="14" y="14" width="7" height="7"></rect><rect x="3" y="14" width="7" height="7"></rect></svg>
              <svg :class="{ active: !grid }" @click="grid = !true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="8" y1="6" x2="21" y2="6"></line><line x1="8" y1="12" x2="21" y2="12"></line><line x1="8" y1="18" x2="21" y2="18"></line><line x1="3" y1="6" x2="3" y2="6"></line><line x1="3" y1="12" x2="3" y2="12"></line><line x1="3" y1="18" x2="3" y2="18"></line></svg>
            </div>
          </div>

          <notes :notes="notesFilter" :grid="grid" @remove="removeNote" @edit="editTitle" @update="updateTitle" @notupdate="notUpdateTitle" />

        </div>
      </section>
    </div>

    <!-- <footer></footer> -->

  </div>

</template>

<script>

import message from '@/components/Message.vue'
import newNote from '@/components/NewNote.vue'
import notes from '@/components/Notes.vue'
import search from '@/components/Search.vue'

export default {
  data () {
    return {
      title: 'Notes app',
      search: '',
      message: null,
      grid: true,
      note: {
        title: '',
        descr: '',
        editable: true,
        selected: 1,
        statuses: [
          { text: 'Standart', value: 1 },
          { text: 'Middle', value: 2 },
          { text: 'Hot', value: 3 }
        ]
      },
      notes: [
        {
          title: 'Title 0',
          descr: 'Description text 0',
          date: new Date(Date.now()).toLocaleString(),
          editable: true,
          titleOrigin: 'Title 0',
          descrOrigin: 'Description text 0',
          selected: 1,
        },
        {
          title: 'Title 1',
          descr: 'Description text 1',
          date: new Date(Date.now()).toLocaleString(),
          editable: true,
          titleOrigin: 'Title 1',
          descrOrigin: 'Description text 1',
          selected: 1,
        }
      ],
    }
  },
  computed: {
    notesFilter () {
      let array = this.notes,
          search = this.search

      if (!search) return array

      search = search.trim().toLowerCase()

      array = array.filter(function (item) {
        if (item.title.toLowerCase().indexOf(search) !== -1) {
          return item
        }
      })

      return array

    }
  },
  methods: {
    addNote () {
      let {title, descr, selected} = this.note

      if (title === '') {
        this.message = 'this input can`t be blank!'
        return false
      }

      this.notes.push({
        title,
        descr,
        date: new Date(Date.now()).toLocaleString(),
        editable: true,
        //titleOrigin: title,
        //descrOrigin: descr,
        selected,
      })

      this.message = null
      this.note.title = ''
      this.note.descr = ''
      this.note.selected = 1

    },
    removeNote (index) {
      this.notes.splice(index, 1)
    },
    editTitle (note) {
      note.editable = false
      note.titleOrigin = note.title
      note.descrOrigin = note.descr
      //console.log(note)
    },
    updateTitle (note) {
      note.editable = true
      note.date = new Date(Date.now()).toLocaleString()
      //note.title = 'ooooook'
      //console.log(note)
    },
    notUpdateTitle (note) {
      note.editable = true
      note.title = note.titleOrigin
      note.descr = note.descrOrigin
      //note.title = 'ooooook'
      //console.log(note)
    }
  },
  components: {
    message,
    newNote,
    notes,
    search,
  }
}

</script>

<style lang="scss">
.title {
  font-size: 36px;
  margin: 20px 0;
}
</style>
