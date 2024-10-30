<script lang="ts">
    import type { Snippet } from 'svelte';
    import type { Action } from 'svelte/action';
    let props: { children: Snippet, action: Action, open: boolean } = $props();
</script>

<button use:props.action>
    <div class="wrapper">
        <svg viewBox="0 0 100 100">            
            {#if props.open}
            <path d="M30,40 L50,60 L70,40" x1="40" y1="30" x2="60" y2="50" />
            {:else}
            <path d="M40,30 L60,50 L40,70" x1="40" y1="30" x2="60" y2="50" />
            {/if}
        </svg>    
    </div> 
    {@render props.children()}
</button>

<style>    
    button {
        padding: 0;
        background: none;
        border: none;
        color: inherit;
        display: flex;
        white-space: nowrap;
        gap: 3px;
        outline: none;
    }

    .wrapper {
        width: 19px;
        height: 19px;
        border: 1px solid #666;
        border-radius: 9.5px;
        background: #DDDDDD;
    }

    svg {
        width: 18px;
        height: 18px;
        stroke: #666;
        stroke-width: 10;
        fill: none;
    }

    button:hover {
        &>.wrapper {
            border-color: #222;
        }
        &>.wrapper>svg {
            stroke: #222;
        }
    }

    button:focus, button:focus-visible {
        &>.wrapper {
            background-color: #26A0DA;
            border-color: #26A0DA;
        }
    }
</style>