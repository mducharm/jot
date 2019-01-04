<template>
  <div class="menu-container">
    <div class="menu-options">
      <button class="btn btn-dark logo">
        <!-- <i class="material-icons md-light">edit</i> -->
        <h2 class="logo-text">jot</h2>
      </button>
      <button @click="$emit('settings')" class="btn btn-light settingsBtn">
        <i class="material-icons">build</i>
      </button>
      <button @click="toggleDeleting" class="btn btn-light deleteBtn">
        <i class="material-icons">clear</i>
      </button>
      <button @click="toggleAdding" class="btn btn-light addBtn">
        <i class="material-icons">add</i>
      </button>
      <input
        class="addTextBox"
        v-show="adding"
        @keyup.enter="$emit('addNote', inputText); inputText = ''"
        v-model="inputText"
      >
    </div>
    <ul>
      <li v-for="(note, index) in notes" :key="note" @click="updateActiveNote(index)">
        {{note.title}}
        <button
          v-show="deleting"
          @click.stop="$emit('deleteNote', index)"
          class="btn btn-danger"
        >
          <i class="material-icons">clear</i>
        </button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "MainMenu",
  props: ["notes"],
  data() {
    return {
      editing: false,
      adding: false,
      deleting: false,
      inputText: ""
    };
  },
  methods: {
    updateActiveNote(ind) {
      this.$emit("noteSelected", ind);
    },
    toggleEditing() {
      if (this.editing) {
        this.editing = false;
      } else {
        this.editing = true;
      }
    },
    toggleAdding() {
      if (this.adding) {
        this.adding = false;
      } else {
        this.adding = true;
      }
    },
    toggleDeleting() {
      if (this.deleting) {
        this.deleting = false;
      } else {
        this.deleting = true;
      }
    }
  }
};
</script>

<style scoped>
.menu-container {
  display: grid;
  margin-top: 0;
  padding: 10px;
  /* border: solid 0.5px #888888;
  border-radius: 5px;
  box-shadow: 3px 3px 8px #888888; */
}

.menu-options {
  display: grid;
  margin-top: 0;
  padding: 10px;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  grid-template-rows: auto;
  grid-template-areas:
    "logo settings delete addBtn"
    "addBox addBox addBox addBox";
}

.logo {
  grid-area: logo;
  border: solid 0.5px #c2c2c2;
  border-radius: 5px;
  padding: 10px;
  text-align: center;
}

.logo-text {
  font-family: 'Pacifico', cursive;
  float: right;
  color: white;
}

.settingsBtn {
  grid-area: settings;
  border: solid 0.5px #c2c2c2;
  border-radius: 5px;
}
.deleteBtn {
  grid-area: delete;
  border: solid 0.5px #c2c2c2;
  border-radius: 5px;
}
.addBtn {
  grid-area: addBtn;
  border: solid 0.5px #c2c2c2;
  border-radius: 5px;
}

.addTextBox {
  grid-area: addBox;
  text-align: center;
  margin-top: 5%;
  padding: 10px 10px 10px 10px;
}

ul {
  padding: 0;
  list-style-type: none;
}

li {
  list-style: none;
  padding: 20px 20px;
  margin: 2px;
  border: solid 0.5px #c2c2c2;
  border-radius: 5px;
  width: 100%;
  font-family: 'Asap', sans-serif;
}
</style>
