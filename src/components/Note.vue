<template>
  <div class="note-container">
    <button @click="$emit('back')" class="btn btn-light backBtn"><i class="material-icons">arrow_back</i></button>
    <!-- <input type="text" :value="noteData[activeNote].title" @keyup="$emit('editTitle')"> -->
    <input
      type="text"
      class="title"
      :value="noteData[activeNote].title"
      @input="noteData[activeNote].title = $event.target.value"
    >
    <textarea
      class="note"
      cols="30"
      rows="15"
      :value="noteData[activeNote].content"
      @input="noteData[activeNote].content = $event.target.value"
    ></textarea>
  </div>
</template>

<script>
export default {
  name: "Note",
  props: ["activeNote", "noteData"],
  data() {
    return {};
  },
  computed() {
    return {
      // titleText: this.noteData[activeNote].title,
      // contentText: this.noteData[activeNote].content
    };
  }
};
</script>

<style scoped>
.note-container {
  display: grid;
  margin-top: 0;
  padding: 10px;
  grid-template-columns: 20% 80%;
  grid-template-rows: auto;
  grid-template-areas:
    "back ."
    "title title"
    "note note";
  /* border: solid 0.5px #888888;
  border-radius: 5px;
  box-shadow: 3px 3px 8px #888888; */
}

.backBtn {
  grid-area: back;
  border: solid 0.5px #c2c2c2;
}

.title {
  grid-area: title;
  text-align: center;
  margin-top: 5%;
  padding: 10px 10px 10px 10px;
  font-family: 'Asap', sans-serif;
}

.note {
  grid-area: note;
}

textarea {
  background-color: #fff;
  background-image: 
/* linear-gradient(90deg, transparent 79px, #abced4 79px, #abced4 81px, transparent 81px), */ linear-gradient(
    #eee 0.1em,
    transparent 0.1em
  );
  background-size: 100% 2em;
  background-attachment: local;
  border-radius: 5px;
  margin-top: 5%;
  line-height: 2em;
  padding-right: 5px;
  padding-left: 5px;
  font-family: 'Asap', sans-serif;
}
</style>
