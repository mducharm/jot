<template>
  <div class="settings-container">
    <button @click="$emit('back')" class="btn btn-light backBtn">
      <i class="material-icons">arrow_back</i>
    </button>
    <button class="btn btn-light exportBtn" @click="$emit('export')">Export</button>
    <button class="btn btn-danger delBtn" @click="confirmDelete = true">Delete All</button>
    <div v-show="confirmDelete" class="confirmDeleteDialog">
      <h3>Are you sure?</h3>
      <button @click="$emit('deleteAll'); confirmDelete = false" class="btn btn-danger">Yes</button>
      <button @click="confirmDelete = false" class="btn noBtn">No</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Settings",
  data() {
    return {
      confirmDelete: false
    };
  }
};
</script>

<style scoped>
.settings-container {
  display: flex;
  flex-flow: column nowrap;
  justify-content: center;
}

.exportBtn {
  width: 100%;
  border: solid 0.5px #c2c2c2;
  border-radius: 5px;
}

.delBtn {
  width: 100%;
}

.backBtn {
  border: solid 0.5px #c2c2c2;
  border-radius: 5px;
  margin-bottom: 30px;
}

.confirmDeleteDialog {
  margin-top: 10%;
}

.noBtn {
  border: solid 0.5px #c2c2c2;
  border-radius: 5px;
}
</style>
