<script lang="ts">
    import type { Snippet } from "svelte";    
    let props: { children: Snippet } = $props();
  </script>
  
  <div class="panel">
    {@render props.children()}
  </div>
  
  <style>
    .panel {
        gap: 20px;
        padding: 20px;
        display: flex;
        flex-direction: row;
        align-items: start;
    }

    .panel > :global(*) {
        width: 600px;
    }
  </style>