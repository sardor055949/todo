<template>
  <Navbar
    @searchValue="search = $event"
    @searchOpen="searchOpen"
    @searchClose="searchClose"
    :lang="lang"
    @changeLang="changeLang"
  />
  <Notes
    :notes="filterNotes"
    @delNote="delNote"
    @changeNote="changeNote"
    :searchOn="searchOn"
    :lang="lang"
  />
  <Modal
    v-show="modalOpen"
    @closeModal="closeModal"
    :currentId="currentId"
    @addNote="addNote"
    :edit="edit"
    :editNote="editNote"
    @editedNote="editedNote"
    :lang="lang"
  />
  <ModalBtn @openModal="openModal" />
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import Notes from "@/components/Notes.vue";
import Modal from "@/components/Modal.vue";
import ModalBtn from "@/components/ModalBtn.vue";
import langs from "@/lang";
export default {
  components: {
    Navbar,
    Notes,
    Modal,
    ModalBtn,
  },
  created() {
    this.getNotes();
    localStorage.lang = localStorage.lang || "ru"
    this.lang = localStorage.lang || "ru"
    this.langwords = langs
    localStorage.words = JSON.stringify(this.langwords);
  },
  data() {
    return {
      notes: [],
      modalOpen: false,
      currentId: 1,
      edit: false,
      editNote: {},
      search: "",
      searchOn: false,
      lang: "ru",
      langwords: {},
    };
  },
  computed: {
    filterNotes() {
      return this.search
        ? this.notes.filter((note) =>
            note.title.toLowerCase().includes(this.search.toLowerCase())
          )
        : this.notes;
    },
  },
  watch: {
    notes: {
      handler(newNotes) {
        localStorage.notes = JSON.stringify(this.notes);
      },
      deep: true,
    },
  },
  methods: {
    getNotes() {
      let localNotes = localStorage.notes;
      if (localNotes) {
        this.notes = JSON.parse(localNotes);
      }
    },
    openModal() {
      this.modalOpen = true;
    },
    closeModal(status) {
      this.modalOpen = status;
    },
    addNote(note) {
      this.notes.push(note);
      this.modalOpen = false;
    },
    delNote(id) {
      let index = this.notes.findIndex((note) => note.id === id);
      this.notes.splice(index, 1);
    },
    changeNote(id) {
      this.modalOpen = this.edit = true;
      let pickedNote = this.notes.find((note) => id === note.id);
      this.editNote = pickedNote;
    },
    editedNote(noteEdited) {
      this.notes.forEach((note) => {
        if (noteEdited.id === note.id) {
          note.title = noteEdited.title;
          note.text = noteEdited.text;
          note.date = noteEdited.date;
        }
      });
      this.modalOpen = this.edit = false;
    },
    searchOpen() {
      this.searchOn = true;
    },
    searchClose() {
      this.searchOn = false;
    },
    changeLang(val) {
      this.lang = localStorage.lang = val;
    },
  },
  provide() {
    return {
        words: localStorage.words ? JSON.parse(localStorage.words) : {}
    }
  }
};
</script>

<style>
</style>
