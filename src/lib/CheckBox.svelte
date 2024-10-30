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

<div class="wrapper">
    <button use:melt={$root}>
        <svg viewBox="0 0 130 120">            
            {#if $isChecked}
            <path d="M20,55 L55,85 L100,15"/>
            {/if}
        </svg>
        <input use:melt={$input} id="{props.id}" />
    </button>
</div>

<style>
    .wrapper {
        height: 22px;
        display: flex;        
        align-items: center;
    }
    
    button {
        width: 14px;
        height: 13px;
        padding: 0;
        background: white;
        border: 1px solid #ABADB3;
        outline: none;
        &:hover, &:focus-visible {
            border-color: #569DE5;
        }
    }

    svg {
        width: 13px;
        height: 12px;
        stroke: #000;
        stroke-width: 20;
        fill: none;
    }
</style>