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
      content: `
            <h2>
              Hi there 👋
            </h2>
          `,
      onTransaction: () => {
        editor = editor;
      },

      editorProps: {
        attributes: {
          class:
            "prose prose-sm sm:prose lg:prose-lg xl:prose-2xl mx-auto focus:outline-none",
        },
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
  <div class="flex gap-4">
    <button
      on:click={() => editor.chain().focus().toggleHeading({ level: 1 }).run()}
      class={editor.isActive("heading", { level: 1 }) ? "is-active" : ""}
    >
      h1
    </button>

    <button
      on:click={() => editor.chain().focus().toggleBold().run()}
      class:active={editor.isActive("paragraph")}
    >
      Bold
    </button>
  </div>
{/if}

<div class="shadow-xl rounded-md">
  <div class=" p-16" bind:this={element}></div>
</div>
