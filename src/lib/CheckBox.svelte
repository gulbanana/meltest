<script lang="ts">
    import { createCheckbox, melt } from '@melt-ui/svelte'

    let props: { id: string, value: boolean } = $props();
    let {
        elements: { root, input },
        helpers: { isChecked, isIndeterminate },
    } = createCheckbox({
        defaultChecked: props.value,
    });
</script>

<button use:melt={$root}>
    <svg viewBox="0 0 200 200">            
        {#if $isChecked}
        <path d="M30,122 L80,170 L170,20" stroke-linecap="round"/>
        {/if}
    </svg>
    <input use:melt={$input} id="{props.id}" />
</button>

<style>
    button {
        width: 22px;
        height: 22px;
        padding: 0;
        background: white;
        border: 1px solid #ABADB3;
        &:hover, &:focus-visible {
            border-color: #569DE5;
        }
    }

    svg {
        width: 20px;
        height: 20px;
        stroke: #000;
        stroke-width: 25;
        fill: none;
    }
</style>