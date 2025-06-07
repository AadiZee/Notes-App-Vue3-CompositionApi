<script setup>
import { ref } from "vue";

const showModal = ref(false);
const newNote = ref("");
const notes = ref([]);

const addNote = () => {
  if (!newNote.value) {
    alert("No note description added!");
    return;
  }
  notes.value.push({
    id: notes.value.length + 1,
    text: newNote.value,
    date: new Date(),
    backgroundColor: "hsl(" + Math.random() * 360 + ", 100%, 75%",
  });
  newNote.value = "";
  showModal.value = false;
  console.log(notes);
};
</script>

<template>
  <main>
    <div v-if="showModal" class="overlay">
      <div class="modal">
        <div class="modal-header">
          <h2>Add new note</h2>
          <button class="close" @click="showModal = false">X</button>
        </div>
        <textarea
          v-model="newNote"
          name="notes"
          id="notes"
          rows="10"
          cols="100"
        ></textarea>
        <button class="add" @click="addNote">Add note</button>
      </div>
    </div>

    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showModal = true">+</button>
      </header>

      <div v-if="notes.length === 0" class="no-notes-container">
        <h3 class="no-notes-message">
          No notes added. Click on the + button to start adding notes
        </h3>
      </div>

      <div v-if="notes.length > 0" class="cards-container">
        <div
          v-for="note in notes"
          class="card"
          :style="{ backgroundColor: note?.backgroundColor }"
          :key="note.id"
        >
          <p class="main-text">
            {{ note.text }}
          </p>
          <p class="date">{{ note.date.toLocaleDateString("en-US") }}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
main {
  height: 100vh;
  width: 100vw;
}

.container {
  max-width: 1000px;
  padding: 10px;
  margin: 0 auto;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

header h1 {
  font-weight: bold;
  margin-bottom: 25px;
  font-size: 75px;
}

header button {
  border: none;
  padding: 10px;
  width: 50px;
  height: 50px;
  cursor: pointer;
  background-color: rgb(21, 20, 20);
  border-radius: 100%;
  color: white;
  font-size: 25px;
}

.card {
  width: 225px;
  height: 225px;
  background-color: rgb(237, 182, 44);
  padding: 10px;
  border-radius: 15px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-right: 20px;
  margin-bottom: 20px;
}

.date {
  font-size: 12.5px;
  font-weight: bold;
}

.cards-container {
  display: flex;
  flex-wrap: wrap;
}

.overlay {
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.75);
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal {
  width: 750x;
  background-color: white;
  border-radius: 10px;
  padding: 30px;
  position: relative;
  display: flex;
  flex-direction: column;
}

.add {
  padding: 10px 20px;
  font-size: 20px;
  width: 100%;
  background-color: blueviolet;
  margin-top: 15px;
  color: white;
  cursor: pointer;
  border: none;
}

.modal-header {
  display: flex;
  width: 100%;
  justify-content: space-between;
  align-items: center;
  font-weight: 100;
}

.close {
  margin-top: 0px;
  cursor: pointer;
  border: none;
  border-radius: 100%;
  padding: 5px;
  background-color: transparent;
  color: red;
}

.modal-header h2 {
  margin-top: 0px;
  font-weight: 100;
}

.no-notes-container {
  text-align: center;
}

.no-notes-message {
  font-weight: 100;
}
</style>
