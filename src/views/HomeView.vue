<template>
  <editor-content class="grow flex flex-col" v-if="editor" :editor="editor" />
</template>

<script setup lang="ts">
import { onBeforeUnmount, onMounted } from "vue";
import { Editor, EditorContent, useEditor } from "@tiptap/vue-3";
import Document from "@tiptap/extension-document";
import Paragraph from "@tiptap/extension-paragraph";
import TaskItem from "@tiptap/extension-task-item";
import TaskList from "@tiptap/extension-task-list";
import ListItem from "@tiptap/extension-list-item";
import OrderedList from "@tiptap/extension-ordered-list";
import BulletList from "@tiptap/extension-bullet-list";
import Text from "@tiptap/extension-text";

const editor = useEditor({
  extensions: [
    Document,
    Paragraph,
    Text,
    OrderedList,
    BulletList,
    ListItem,
    TaskList,
    TaskItem.configure({
      nested: true,
    }),
  ],
  content: `
          <p>Welcome to a new note</p>
          <p></p>
          <p>Create a new task list by typing [ ] or [x]</p>
        `,
});
</script>

<style lang="scss" scoped>
ul[data-type="taskList"] {
  list-style: none;
  padding: 0;

  p {
    margin: 0;
  }

  li {
    display: flex;

    > label {
      flex: 0 0 auto;
      margin-right: 0.5rem;
      user-select: none;
    }

    > div {
      flex: 1 1 auto;
    }
  }
}

> * + * {
  margin-top: 0.75em;
}

ul,
ol {
  padding: 0 1rem;
}
</style>
