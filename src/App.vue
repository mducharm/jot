<template>
  <div id="app">
    <div class="container">
      <MainMenu
        :notes="noteData"
        :activeNote="activeNote"
        @addNote="createNote($event); save()"
        @deleteNote="deleteNote($event); save()"
        @noteSelected="setNote($event)"
        @settings="showSettings = true"
        v-show="!showSettings && activeNote === -1"
      />
      <Note
        @back="activeNote = -1"
        @update="save()"
        v-show="activeNote !== -1 && !showSettings"
        :activeNote="activeNote"
        :noteData="noteData"
      />
      <Settings
        v-show="showSettings"
        @back="showSettings = false"
        @export="exportNotes"
        @deleteAll="deleteAll"
      />
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
          title: "Welcome to Jot",
          content:
            "Notes are saved automatically, so simply start typing. You can add or delete notes from the main menu options.\n\nUnder Settings, you can also export your notes into a .txt or delete all your notes at once.\n\n For more information, go to https://github.com/mducharm/jot"
        }
      ]
    };
  },
  mounted () {
    if (localStorage.getItem("noteData")) {
      this.noteData = JSON.parse(localStorage.getItem("noteData"))
    }
  },
  methods: {
    createNote(t) {
      var note = {
        title: t,
        content: ""
      };
      this.$set(this.noteData, this.noteData.length, note);
    },
    deleteNote(index) {
      this.$delete(this.noteData, index);
    },
    setNote(note) {
      this.activeNote = note;
    },
    exportNotes() {
      // var dataStr = "data:text/txt; charset=utf-8," + encodeURIComponent(JSON.stringify(this.noteData));
      var dataStr = "data:text/plain; charset=utf-8,";
      this.noteData.forEach(
        x =>
          (dataStr += encodeURIComponent(
            x.title + "\r\n" + x.content + "\r\n\r\n"
          ))
      );
      var downloadAnchorNode = document.createElement("a");
      downloadAnchorNode.setAttribute("href", dataStr);
      downloadAnchorNode.setAttribute("download", "notes.txt");
      document.body.appendChild(downloadAnchorNode);
      downloadAnchorNode.click();
      downloadAnchorNode.remove();
    },
    deleteAll() {
      this.noteData = [];
    },
    save() {
      localStorage.setItem("noteData", JSON.stringify(this.noteData))
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
