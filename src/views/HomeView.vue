<template>
  <div v-if="editor">
    <editor-content :editor="editor" />
  </div>
</template>

<script lang="ts">
import Document from "@tiptap/extension-document";
import Paragraph from "@tiptap/extension-paragraph";
import TaskItem from "@tiptap/extension-task-item";
import TaskList from "@tiptap/extension-task-list";
import Text from "@tiptap/extension-text";
import { Editor, EditorContent } from "@tiptap/vue-3";

export default {
  components: {
    EditorContent,
  },

  data() {
    return {
      editor: null as Editor | null,
    };
  },

  mounted() {
    this.editor = new Editor({
      extensions: [
        Document,
        Paragraph,
        Text,
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
  },

  beforeUnmount() {
    this.editor?.destroy();
  },
};
</script>

<style lang="scss">
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
</style>
