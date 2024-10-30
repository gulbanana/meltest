<script lang="ts">
    import CheckBox from "$lib/CheckBox.svelte";
    import DateBox from "$lib/DateBox.svelte";
    import Field from "$lib/Field.svelte";
    import Panel from "$lib/Panel.svelte";
    import Section from "$lib/Section.svelte";  
    import TextBox from "$lib/TextBox.svelte";
</script>

<Panel>
    <Section header="Main Detail">
        <Field label="Christian* Name">
            {#snippet children(id)}
                <TextBox {id} value="Thomas" />
            {/snippet}
        </Field>
        <Field label="Surname">
            {#snippet children(id)}
                <TextBox {id} value="Castiglione" />
            {/snippet}
        </Field>
    </Section>
    <Section header="Exotic Fields">
        <Field label="Is Checkbox">
            {#snippet children(id)}
                <CheckBox {id} value={true} />
            {/snippet}
        </Field>
        <Field label="Event Date">
            {#snippet children(id)}
                <DateBox {id} />
            {/snippet}
        </Field>
    </Section>
</Panel>