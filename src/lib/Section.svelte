<script lang="ts">
    import type { Snippet } from "svelte";
    import { createCollapsible, melt } from "@melt-ui/svelte";
    import Toggle from "./Toggle.svelte";
    
    let props: { children: Snippet, header: string } = $props();
    let {
      elements: { root, content, trigger },
      states: { open },
    } = createCollapsible();
    $open = true;
</script>
  
<div class="box" use:melt={$root}>
    <header>
        <Toggle {...$trigger} open={$open}>{props.header}</Toggle>
    </header>

    <div class="content" use:melt={$content}>
        {@render props.children()}
    </div>
</div>

<style>
    .box {
        border: 1px solid;
        border-image: var(--gradient-border) 1;
    }

    header {
        padding: 1px;

        display: grid;
        grid-template-columns: 1fr;
        grid-template-rows: 23px;
        align-items: center;

        background: var(--gradient-bar);
        color: #ffffff;
    }

    .content {
        background: #ffffff;
        padding: 2px;
        display: flex;
        flex-direction: column;
    }
</style>