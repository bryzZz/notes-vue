<script setup lang="ts">
import { computed } from "vue";
import { Note } from "../types";

const props = defineProps<{
  notes: Note[];
  onDelete: (note: Note) => void;
  onPin: (note: Note) => void;
}>();

const pinnedNotes = computed(() => props.notes.filter((note) => note.pinned));
const unpinnedNotes = computed(() =>
  props.notes.filter((note) => !note.pinned)
);

console.log(props.notes);
</script>

<template>
  <div class="notes__container">
    <div v-if="pinnedNotes.length > 0">
      <p class="notes__pinned">Pinned:</p>
      <div class="notes">
        <div class="note" v-for="note in pinnedNotes">
          <div class="note__button note__pin" @click="() => onPin(note)">
            <svg
              id="Layer_1"
              style="enable-background: new 0 0 91 91"
              version="1.1"
              viewBox="0 0 91 91"
              xml:space="preserve"
              xmlns="http://www.w3.org/2000/svg"
              xmlns:xlink="http://www.w3.org/1999/xlink"
            >
              <g>
                <path
                  d="M31.7,54.2h13.6v21.5h3.4V54.2h13.6c0.9,0,1.7-0.8,1.7-1.7v-4.7c0-3.4-2.6-6.3-5.9-6.7l-1-8.7c-0.1-0.8-0.8-1.5-1.7-1.5   c0,0,0,0,0,0l-16.7,0c-0.9,0-1.6,0.6-1.7,1.5l-1,8.6c-3.3,0.4-5.9,3.2-5.9,6.7v4.7C30,53.5,30.8,54.2,31.7,54.2z"
                />
                <path
                  d="M35.9,28.6h22.2c0.9,0,1.7-0.8,1.7-1.7v-3.6c0-3-2.5-5.5-5.5-5.5H39.7c-3,0-5.5,2.5-5.5,5.5v3.6   C34.2,27.9,35,28.6,35.9,28.6z"
                />
              </g>
            </svg>
          </div>
          <div class="note__content">
            <h4 class="note__title">{{ note.title }}</h4>
            <p class="note__title">{{ note.text }}</p>
          </div>
          <div class="note__controls">
            <div class="note__button note__trash" @click="() => onDelete(note)">
              <svg viewBox="0 0 512 512" xmlns="http://www.w3.org/2000/svg">
                <g data-name="1" id="_1">
                  <path
                    d="M356.65,450H171.47a41,41,0,0,1-40.9-40.9V120.66a15,15,0,0,1,15-15h237a15,15,0,0,1,15,15V409.1A41,41,0,0,1,356.65,450ZM160.57,135.66V409.1a10.91,10.91,0,0,0,10.9,10.9H356.65a10.91,10.91,0,0,0,10.91-10.9V135.66Z"
                  />
                  <path
                    d="M327.06,135.66h-126a15,15,0,0,1-15-15V93.4A44.79,44.79,0,0,1,230.8,48.67h66.52A44.79,44.79,0,0,1,342.06,93.4v27.26A15,15,0,0,1,327.06,135.66Zm-111-30h96V93.4a14.75,14.75,0,0,0-14.74-14.73H230.8A14.75,14.75,0,0,0,216.07,93.4Z"
                  />
                  <path
                    d="M264.06,392.58a15,15,0,0,1-15-15V178.09a15,15,0,1,1,30,0V377.58A15,15,0,0,1,264.06,392.58Z"
                  />
                  <path
                    d="M209.9,392.58a15,15,0,0,1-15-15V178.09a15,15,0,0,1,30,0V377.58A15,15,0,0,1,209.9,392.58Z"
                  />
                  <path
                    d="M318.23,392.58a15,15,0,0,1-15-15V178.09a15,15,0,0,1,30,0V377.58A15,15,0,0,1,318.23,392.58Z"
                  />
                  <path
                    d="M405.81,135.66H122.32a15,15,0,0,1,0-30H405.81a15,15,0,0,1,0,30Z"
                  />
                </g>
              </svg>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="notes">
      <div class="note" v-for="note in unpinnedNotes">
        <div class="note__button note__pin" @click="() => onPin(note)">
          <svg
            id="Layer_1"
            style="enable-background: new 0 0 91 91"
            version="1.1"
            viewBox="0 0 91 91"
            xml:space="preserve"
            xmlns="http://www.w3.org/2000/svg"
            xmlns:xlink="http://www.w3.org/1999/xlink"
          >
            <g>
              <path
                d="M31.7,54.2h13.6v21.5h3.4V54.2h13.6c0.9,0,1.7-0.8,1.7-1.7v-4.7c0-3.4-2.6-6.3-5.9-6.7l-1-8.7c-0.1-0.8-0.8-1.5-1.7-1.5   c0,0,0,0,0,0l-16.7,0c-0.9,0-1.6,0.6-1.7,1.5l-1,8.6c-3.3,0.4-5.9,3.2-5.9,6.7v4.7C30,53.5,30.8,54.2,31.7,54.2z"
              />
              <path
                d="M35.9,28.6h22.2c0.9,0,1.7-0.8,1.7-1.7v-3.6c0-3-2.5-5.5-5.5-5.5H39.7c-3,0-5.5,2.5-5.5,5.5v3.6   C34.2,27.9,35,28.6,35.9,28.6z"
              />
            </g>
          </svg>
        </div>
        <div class="note__content">
          <h4 class="note__title">{{ note.title }}</h4>
          <p class="note__title">{{ note.text }}</p>
        </div>
        <div class="note__controls">
          <div class="note__button note__trash" @click="() => onDelete(note)">
            <svg viewBox="0 0 512 512" xmlns="http://www.w3.org/2000/svg">
              <g data-name="1" id="_1">
                <path
                  d="M356.65,450H171.47a41,41,0,0,1-40.9-40.9V120.66a15,15,0,0,1,15-15h237a15,15,0,0,1,15,15V409.1A41,41,0,0,1,356.65,450ZM160.57,135.66V409.1a10.91,10.91,0,0,0,10.9,10.9H356.65a10.91,10.91,0,0,0,10.91-10.9V135.66Z"
                />
                <path
                  d="M327.06,135.66h-126a15,15,0,0,1-15-15V93.4A44.79,44.79,0,0,1,230.8,48.67h66.52A44.79,44.79,0,0,1,342.06,93.4v27.26A15,15,0,0,1,327.06,135.66Zm-111-30h96V93.4a14.75,14.75,0,0,0-14.74-14.73H230.8A14.75,14.75,0,0,0,216.07,93.4Z"
                />
                <path
                  d="M264.06,392.58a15,15,0,0,1-15-15V178.09a15,15,0,1,1,30,0V377.58A15,15,0,0,1,264.06,392.58Z"
                />
                <path
                  d="M209.9,392.58a15,15,0,0,1-15-15V178.09a15,15,0,0,1,30,0V377.58A15,15,0,0,1,209.9,392.58Z"
                />
                <path
                  d="M318.23,392.58a15,15,0,0,1-15-15V178.09a15,15,0,0,1,30,0V377.58A15,15,0,0,1,318.23,392.58Z"
                />
                <path
                  d="M405.81,135.66H122.32a15,15,0,0,1,0-30H405.81a15,15,0,0,1,0,30Z"
                />
              </g>
            </svg>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
@import "../vars.scss";

.notes {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  margin-bottom: 2rem;

  &__pinned {
    font-size: 1.2rem;
    color: rgba(255, 255, 255, 0.87);
    margin-bottom: 0.5rem;
  }
}

.note {
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  width: 15rem;
  height: 7rem;
  padding: 0.3rem;
  border: 1px solid $border-color;
  border-radius: 0.5rem;
  color: #fff;
  font-size: 1.2rem;

  &__title {
    line-height: 0.9;
  }

  &__title,
  &__text {
    padding-left: 0.5rem;
    padding-top: 0.5rem;
  }

  &__controls {
    display: flex;
    justify-content: flex-end;
    opacity: 0;
    transition: opacity 0.3s ease-in-out;
  }

  &:hover &__controls {
    opacity: 1;
  }

  &__button {
    display: grid;
    place-items: center;
    width: 1.8rem;
    height: 1.8rem;
    border-radius: 50%;
    cursor: pointer;

    &:hover {
      background-color: $bg-color-hover;
    }

    & svg {
      width: 70%;
      height: 70%;
      fill: currentColor;
    }
  }

  &__pin {
    position: absolute;
    right: 0.3rem;
    top: 0.3rem;
    width: 2rem;
    height: 2rem;

    & svg {
      width: 80%;
      height: 80%;
    }
  }
}
</style>
