<script lang="ts">
  import { onDestroy, onMount } from "svelte";
  import { Editor } from "@tiptap/core";
  import StarterKit from "@tiptap/starter-kit";

  let element: HTMLDivElement;
  let editor: Editor;

  onMount(() => {
    editor = new Editor({
      element: element,
      extensions: [StarterKit],
      content: "",
      onTransaction: () => {
        editor = editor;
      },
    });
  });

  onDestroy(() => {
    if (editor) {
      editor.destroy();
    }
  });
</script>

{#if editor}
  <button on:click={() => editor.chain().focus().setParagraph().run()}>
    H1
  </button>

  <button
    on:click={() => editor.chain().focus().setParagraph().run()}
    class:active={editor.isActive("paragraph")}
  >
    P
  </button>
{/if}

<div bind:this={element}></div>
