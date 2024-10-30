<script lang="ts">
    import { CalendarDate } from '@internationalized/date'
    import CheckBox from "$lib/CheckBox.svelte";
    import DateBox from "$lib/DateBox.svelte";
    import Field from "$lib/Field.svelte";
    import Panel from "$lib/Panel.svelte";
    import Section from "$lib/Section.svelte";  
    import TextBox from "$lib/TextBox.svelte";
    import ComboBox from '$lib/ComboBox.svelte';
</script>

<Panel>
    <Section header="Main Detail">
        <Field label="Christian* Name">
            {#snippet content(id)}
                <TextBox {id} value="Thomas" />
            {/snippet}
        </Field>
        <Field label="Surname">
            {#snippet content(id)}
                <TextBox {id} value="Castiglione" />
            {/snippet}
        </Field>
    </Section>
    <Section header="Exotic Fields">
        <Field label="Birthday">
            {#snippet content(id)}
                <DateBox {id} value={new CalendarDate(1984, 10, 13)} />
            {/snippet}
        </Field>
        <Field label="Is Checkbox">
            {#snippet content(id)}
                <CheckBox {id} value={true} />
            {/snippet}
        </Field>
        <Field label="Nullable Date">
            {#snippet content(id)}
                <DateBox {id} />
            {/snippet}
        </Field>
        <Field label="Entity Selector">
            {#snippet content(id)}
                <ComboBox {id} />
            {/snippet}
        </Field>
    </Section>
</Panel>