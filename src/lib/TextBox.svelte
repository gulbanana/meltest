<script lang="ts">
    let props: { id: string, value: string } = $props();
</script>

<input type="text" id={props.id} value={props.value}>

<style>
    input {
        font-weight: bold;
        min-height: 22px;
        border: 1px solid #ABADB3;
        outline: none;
        &:hover, &:focus-visible {
            border-color: #569DE5;
        }
    }
</style>