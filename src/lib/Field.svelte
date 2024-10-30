<script lang="ts" module>
    let counter = 0
</script>

<script lang="ts">
    import type { Snippet } from 'svelte';
    import { createLabel, melt } from '@melt-ui/svelte'

    let id = `field_${counter++}`;
    let props: { label: string, children: Snippet<[string]> } = $props();
    let { elements: { root } } = createLabel();
</script>

<div class="field">
    <label use:melt={$root} for={id}>{props.label}:</label>
    {@render props.children(id)}
</div>

<style>
    .field {
        margin: 2px;
        display: grid;
        grid-template-columns: 100px 1fr;
        align-items: center;
        font-size: 9pt;
    }
</style>