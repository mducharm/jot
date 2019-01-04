<template>
  <div id="app">
    <div class="container">
    <MainMenu
      :notes="noteData"
      :activeNote="activeNote"
      @addNote="createNote($event)"
      @deleteNote="deleteNote($event)"
      @noteSelected="setNote($event)"
      @settings="showSettings = true"
      v-show="!showSettings && activeNote === -1"
    />
    <Note
      @back="activeNote = -1"
      v-show="activeNote !== -1 && !showSettings"
      :activeNote="activeNote"
      :noteData="noteData"
    />
    <Settings v-show="showSettings" @back="showSettings = false"/>
    </div>
  </div>
</template>

<script>
import MainMenu from "./components/MainMenu.vue";
import Note from "./components/Note.vue";
import Settings from "./components/Settings.vue";

export default {
  name: "app",
  components: {
    MainMenu,
    Note,
    Settings
  },
  data() {
    return {
      activeNote: -1,
      inputVisible: false,
      showSettings: false,
      noteData: [
        {
          title: "Test Note",
          content: "Test note content."
        }
      ]
    };
  },
  methods: {
    createNote(t) {
      var note = {
        title: t,
        content: "Content test"
      };
      this.$set(this.noteData, this.noteData.length, note);
    },
    deleteNote(index) {
      this.$delete(this.noteData, index);
    },
    setNote(note) {
      this.activeNote = note;
    }
  }
};
</script>

<style>
body {
  background-color: whitesmoke;
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 10px;
}
</style>
