<script setup lang="ts">
import { ref, watch, onMounted } from "vue";
import { nanoid } from "nanoid";
import { Note } from "./types";
import { STORAGE_KEY } from "./constants";
import Notes from "./components/Notes.vue";
import NoteForm from "./components/NoteForm.vue";

const notes = ref<Note[]>([]);

onMounted(() => {
  if (localStorage.getItem(STORAGE_KEY)) {
    notes.value = JSON.parse(localStorage.getItem(STORAGE_KEY) || "");
  } else {
    localStorage.setItem(STORAGE_KEY, "[]");
  }
});

watch(
  notes,
  (newValue) => localStorage.setItem(STORAGE_KEY, JSON.stringify(newValue)),
  { deep: true }
);

const handleAddNote = (title: string, text: string) => {
  notes.value.push({
    id: nanoid(5),
    title: title,
    text: text,
    pinned: false,
  });
};

const onDeleteNote = (note: Note) => {
  console.log(note.text);
  console.log(notes.value);

  notes.value = notes.value.filter(({ id }) => note.id !== id);
};

const onPinNote = (note: Note) => {
  note.pinned = !note.pinned;
};
</script>

<template>
  <header class="header">
    <div class="container header__container">
      <a href="/" class="logo">Notes App</a>
    </div>
  </header>
  <main class="container main__container">
    <NoteForm :on-add-note="handleAddNote" />
    <Notes :notes="notes" :on-delete="onDeleteNote" :on-pin="onPinNote" />
  </main>
</template>

<style scoped lang="scss">
@import "./vars.scss";

.container {
  max-width: 1130px;
  margin: 0 auto;
  padding: 0 15px;
}

.logo {
  text-decoration: none;
  color: rgba(255, 255, 255, 0.87);
  font-size: 1.5rem;
}

.main__container {
  padding: 2rem 15px 0;
}

.header {
  border-bottom: 1px solid $border-color;
  &__container {
    padding-top: 1rem;
    padding-bottom: 1rem;
  }
}
</style>
