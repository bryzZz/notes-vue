<script setup lang="ts">
import { ref, onMounted } from "vue";

const { onAddNote } = defineProps<{
  onAddNote: (title: string, text: string) => void;
}>();

const title = ref("");
const text = ref("");
const expanded = ref(false);

onMounted(() => {
  document.addEventListener("click", (event: Event) => {
    if (
      !["form__input", "form__submit"].includes(
        (event.target as HTMLDivElement).className
      )
    ) {
      expanded.value = false;
    }
  });
});

const onFirstInputClick = () => {
  expanded.value = true;
};

const onSubmit = () => {
  onAddNote(title.value, text.value);

  title.value = "";
  text.value = "";
};
</script>

<template>
  <form class="form" @submit.prevent="onSubmit">
    <input
      v-if="!expanded"
      @click="onFirstInputClick"
      class="form__input"
      placeholder="Note"
    />
    <div v-else class="form__extended">
      <input v-model="title" class="form__input" placeholder="Note Title" />
      <input v-model="text" class="form__input" placeholder="Note" />
      <button class="form__submit" type="submit">Submit</button>
    </div>
  </form>
</template>

<style scoped lang="scss">
@import "../vars.scss";

.form {
  max-width: 500px;
  margin: 0 auto;
  margin-bottom: 2rem;

  &__extended {
    display: flex;
    flex-direction: column;
    gap: 0.3rem;
  }

  &__input,
  &__submit {
    color: rgba(255, 255, 255, 0.87);
    font-size: 1.2rem;
    border: none;
    border-radius: 0.5rem;
    outline: none;
    padding: 0.8rem;
  }

  &__input {
    width: 100%;
    background-color: transparent;
    padding: 0.8rem 1rem;
    border: 1px solid $border-color;
  }

  &__submit {
    background-color: transparent;
    background-color: tomato;

    cursor: pointer;
  }
}
</style>
